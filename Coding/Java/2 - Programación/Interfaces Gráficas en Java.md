  
Para crear una ventana con interfaz gráfica en Java, puedes utilizar la biblioteca `javax.swing`. Aquí tienes un ejemplo simple de cómo puedes crear una ventana:
```java
import javax.swing.JFrame;
import javax.swing.JLabel;

public class Main {
    public static void main(String[] args) {
        // Crear una instancia de JFrame (ventana)
        JFrame ventana = new JFrame("Mi Ventana");

        // Configurar el tamaño de la ventana
        ventana.setSize(400, 300);

        // Configurar la operación predeterminada al cerrar la ventana
        ventana.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Crear un componente JLabel (etiqueta)
        JLabel etiqueta = new JLabel("¡Hola, mundo!");

        // Agregar la etiqueta a la ventana
        ventana.add(etiqueta);

        // Hacer que la ventana sea visible
        ventana.setVisible(true);
    }
}
```
![[Pasted image 20240304195438.png]]