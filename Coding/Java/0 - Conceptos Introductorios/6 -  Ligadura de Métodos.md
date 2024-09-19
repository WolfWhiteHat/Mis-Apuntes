En Java, la ligadura de métodos se refiere al proceso mediante el cual se determina qué método se debe invocar cuando se llama a un método en una clase que tiene varios métodos con el mismo nombre pero diferentes parámetros.
```java
class Animal {
    void hacerSonido() {
        System.out.println("Animal genérico hace un sonido.");
    }
}

class Perro extends Animal {
    void hacerSonido() {
        System.out.println("El perro ladra.");
    }
}

class Gato extends Animal {
    void hacerSonido() {
        System.out.println("El gato maulla.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal miAnimal;

        miAnimal = new Animal();
        miAnimal.hacerSonido(); // Salida: Animal genérico hace un sonido.

        miAnimal = new Perro();
        miAnimal.hacerSonido(); // Salida: El perro ladra.

        miAnimal = new Gato();
        miAnimal.hacerSonido(); // Salida: El gato maulla.
    }
}
```
En este ejemplo, imagina que `Animal` es como una plantilla básica que tiene una acción llamada `hacerSonido()`. Luego, tenemos dos tipos específicos de animales, `Perro` y `Gato`, que son como versiones más detalladas de `Animal`. Estos tipos especiales de animales tienen su propia manera de hacer sonidos, así que reescriben el método `hacerSonido()` para que se adapte a cómo ladran los perros y cómo maúllan los gatos.

Cuando usamos el método `hacerSonido()` a través de una referencia general a `Animal`, lo que sucede en realidad depende del tipo de animal que esté dentro de esa caja. Si dentro está un perro, escucharás el ladrido del perro. Si es un gato, escucharás el maullido del gato. Esto es lo que queremos decir cuando hablamos de "ligadura dinámica": el programa decide qué acción hacer basándose en el tipo real del animal en ese momento.
![[Pasted image 20240318203430.png]]