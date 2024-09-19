# Instalar Prometheus
Primero instalaremos Prometheus en nuestro sistema
sudo apt install prometheus
![[Pasted image 20231128191503.png]]


# Reiniciaremos los demonio
```
sudo systemctl daemon-reload
```

Iniciaremos el servicio de prometheus
```
sudo systemctl start prometheus.service
```

Verificaremos que este corrindo correctamente el servicio
```
sudo systemctl status prometheus.service
```
![[Pasted image 20231128191902.png]]

# Instalar Grafana
Antes de instalar grafana tendremos que instalar unas dependencias y luego añadir el repositorio final a nuestro sistema
```
sudo apt-get install -y apt-transport-https software-properties-common wget
```
![[Pasted image 20231128192317.png]]

Agregamos las llaves al repositorio
```
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
```
![[Pasted image 20231128192527.png]]

Ahora añadiremos el repositorio
```
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```
![[Pasted image 20231128192734.png]]

Actualizamos y procedemos a instalar grafana
```
sudo apt update
sudo apt install grafana
```
![[Pasted image 20231128192831.png]]

Una vez instalado grafana nos indicara que tenemos que hacer la recarga de los demonios, reiniciamos y habilitaremos el servicio de grafana
```
sudo systemctl daemon-reload
sudo systemctl enable grafana-server
sudo systemctl start grafana-server.service
```
![[Pasted image 20231128193120.png]]


# Configurar Promtheus
Configuraremos el archivo prometheus.yml
```
sudo nano /etc/prometheus/prometheus.yml
```
![[Pasted image 20231128193619.png]]

En este archivo tendremos que añadir las siguientes lineas, en nuestro caso como hemos instalado prometheus desde repositorio ya venia añadido por defecto y no es necesario, si no se ha realizado la instalación simplemente añadimos las lineas marcadas.

Una vez configurado abriremos grafana en el navegador

http://192.168.64.10:3000/login
![[Pasted image 20231128194018.png]]
Por defecto esta configurado por el puerto 3000 y el user y passwd es admin admin, aun que una vez iniciado por primera vez nos pedira que cambiemos la contraseña.

Dentro del menu entraremos en data source
![[Pasted image 20231128194525.png]]

Dentro de data source seleccionaremos Prometheus
![[Pasted image 20231128194502.png]]

Dentro de la configuración de prometheus indicaremos un nombre y abajo configuraremos la URL del servidor que previamente hemos configurado en nuestro archivo prometheus.yml, en caso que nuestro servidor fuera otro añadiriamos la URL del servidor, es decir la ip del servidor y el puerto.
![[Pasted image 20231128194631.png]]

Bajaremos al final de la pagina y seleccionaremos save & test, como podemos ver ya nos salta el mensaje que esta guardado correctamente.
![[Pasted image 20231128195009.png]]

Volvemos a data source y veremos nuestra configuración de prometheus con la ip del servidor
![[Pasted image 20231128195101.png]]


Con esto ya tendremos los 3 servicios funcionando, ahora crearemos un tablero para poder ver todas las métricas

Ahora nos descargaremos un tablero de la pagina de grafana creado por la comunidad.
Para ello vamos a la siguiente URL
https://grafana.com/grafana/dashboards/

Y nos descargaremos el siguiente tablero
https://grafana.com/grafana/dashboards/13978-node-exporter-quickstart-and-dashboard/
![[Pasted image 20231128195742.png]]

Copiaremos el ID

Una vez copiado iremos a import dashboard y pegaremos el ID
![[Pasted image 20231128200257.png]]

![[Pasted image 20231128200351.png]]

Una vez detecte el tablero podremos cambiarle el nombre y añadirlo a una carpeta, una vez definido los parametros le daremos a import

Una vez le demos al import ya podremos ver toda la información monitorizada de nuestro servidor
![[Pasted image 20231128200517.png]]

En la parte de arriba a la derecha podremos configurar los rangos de tiempo que nos aparezcan monitorizado y el tiempo de recarga de la información
![[Pasted image 20231128200617.png]]


### Configurar alertas Prometheus
https://rdavix.medium.com/cómo-exportar-alertas-de-prometheus-en-grafana-157b0482021d

Ahora vamos a proceder a crear alertas en Prometheus
![[Pasted image 20231204081942.png]]
Configuraremos las alertas de Prometheus con Alertmanager, para ello primero necesitaremos instalarlo en nuestro sistema.

### Instalar Alertmanager
Los comandos para instalar alertmanager

sudo apt update -y && sudo apt upgrade
curl -s https://api.github.com/repos/prometheus/alertmanager/releases/latest | grep browser_download_url | grep linux-arm64 | cut -d '"' -f 4 | wget -qi -
tar xvf alertmanager-*.tar.gz 
cd alertmanager*/ 
sudo mv alertmanager /usr/local/bin/ 
sudo mv amtool /usr/local/bin/ 
sudo mkdir /etc/alertmanager 
sudo mv alertmanager.yml /etc/alertmanager 
sudo chown root:root /etc/alertmanager/alertmanager.yml 
sudo chown root:root /usr/local/bin/alertmanager 
sudo chown root:root /usr/local/bin/amtool 
sudo mkdir /var/lib/alertmanager 
sudo chown prometheus:prometheus /var/lib/alertmanager
![[Pasted image 20231204192150.png]]
Descargamos la última versión del AlertManager para ubuntu (amd64) sobre un directorio temporal, lo descomprimimos, movemos los binarios a /usr/local/bin (así lo podemos ejecutar sin añadir nada al PATH), creamos un directorio /etc/alertmanager para almacenar su fichero de configuración, y lo movemos a dicho directorio. También cambiamos el propietario del binario y fichero de configuración, por motivos de seguridad. Por último creamos un directorio para los datos de AlertManager y le cambiamos el propietario.


Comprobamos la version instalada
alertmanager --version
![[Pasted image 20231204192246.png]]


Aprovechamos un momento para revisar el fichero de configuración del AlertManager que incluye por defecto, que viene con una configuración básica, que podemos ir completando y cambiar conforme a nuestras necesidades:

cat /etc/alertmanager/alertmanager.yml
![[Pasted image 20231204085842.png]]



Para poder manejar el AlertManager como un servicio o demonio, vamos a crear su fichero de configuración de systemd, que ejecute el binario con el fichero de configuración que queremos como parámetro y apunte al directorio de datos de AlertManager.
![[Pasted image 20231204092114.png]]
"sudo tee /etc/systemd/system/alertmanager.serviceEOF 
[Unit]
Description=Prometheus AlertManager Documentation=https://github.com/prometheus/alertmanager 
Wants=network-online.target 
After=network-online.target 

[Service] 
Type=simple 
User=prometheus 
Group=prometheus 
ExecReload=/bin/kill -HUP $MAINPID 

ExecStart=/usr/local/bin/alertmanager \ 
	--config.file=/etc/alertmanager/alertmanager.yml \ 
	--storage.path=/var/lib/alertmanager/ \ 
	--web.listen-address=":9093" 
	--cluster.listen-address= 

[Install]
WantedBy=multi-user.target 
EOF

sudo systemctl daemon-reload 
sudo systemctl start alertmanager 
sudo systemctl enable alertmanager 
sudo systemctl status alertmanager
![[Pasted image 20231204192549.png]]
Activamos y arrancamos el servicio de AlertManager


Ahora añadiremos la siguiente información dentro del archivo prometheus.yml
sudo nano /etc/prometheus/prometheus.yml
![[Pasted image 20231204192748.png]]

Comprobamos que el fichero se haya configurado correctamente
promtool check config /etc/prometheus/prometheus.yml
![[Pasted image 20231204193125.png]]

Refrescamos la configuración de prometheus
sudo killall -HUP prometheus

URL para acceder al servicio de prometheus
http://localhost:9093/#/alerts

Ahora vamos a configurar las reglas para monitorizar prometheus
En el siguiente archivo vamos a poder tener reglas para nuestros servicios monitorizados, para eso accederemos a la siguiente ruta y modificaremos el archivo rules.yml
sudo nano /etc/prometheus/rules/rules.yml
![[Pasted image 20231204193856.png]]

Para comprobar que el fichero es correcto podemos utilizar el siguiente comando
promtool check rules /etc/prometheus/rules/rules.yml
![[Pasted image 20231204194156.png]]

Editaremos el fichero /etc/prometheus/prometheus.yml y añadiremos las reglas
... 
rule_files: 
	-rules/rules.yml 
...

Comprobamos que el archivo este bien configurado
promtool check config /etc/prometheus/prometheus.yml
![[Pasted image 20231204194526.png]]


### Revisar logs Prometheus

Para registrar los logs de prometheus primero confirmaremos que tenemos la configuración adecuada, para ello verificaremos que tenemos dentro del archivo scrape_configs configurado
sudo nano /etc/prometheus/prometheus.yml
![[Pasted image 20231204195457.png]]

Una vez comprobado revisaremos los logs con el siguiente comando
tail -f /var/log/prometheus/prometheus.log
![[Pasted image 20231204195755.png]]

En mi caso todavia no hay logs ya que no ha dado tiempo a registrase

Para revisar los registros de Prometheus cuando se ejecuta como un servicio de systemd, puedes utilizar el siguiente comando:
sudo journalctl -u prometheus
![[Pasted image 20231204200305.png]]

Para revisar los loga en tiempo real escribiremos el siguiente comando
sudo journalctl -u prometheus -f
![[Pasted image 20231204200401.png]]




Bibliografia
https://www.youtube.com/watch?v=lbcElrA1Ro8
https://elwillie.es/2022/09/20/prometheus-gestion-de-alertas-con-alertmanager/
https://www.cloudcenterandalucia.es/blog/visualizando-logs-en-grafana/



![[Producto 3. Monitorización de nuestro sistema y análisis de su estado..pdf]]