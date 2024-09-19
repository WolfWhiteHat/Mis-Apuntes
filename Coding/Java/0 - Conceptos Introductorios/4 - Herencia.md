Permite a una clase (llamada clase hija o subclase) heredar atributos y métodos de otra clase (llamada clase padre o superclase), lo que facilita la reutilización de código y la organización jerárquica de las clases.

Cuando una clase hereda de otra, la clase hija adquiere todas las propiedades (métodos y atributos) de la clase padre y puede añadir sus propios métodos o atributos adicionales, o incluso sobrescribir los métodos de la clase padre para adaptarlos a sus necesidades específicas.

La herencia permite la creación de una jerarquía de clases, donde las clases más específicas (hijas) pueden heredar comportamientos y características de las clases más generales (padres), lo que promueve la modularidad, la cohesión y la facilidad de mantenimiento del código.

---------

En este ejemplo, la clase `Animal` es la clase padre o superclase, que define un método `hacerSonido`. La clase `Perro` es la clase hija o subclase que hereda de la clase `Animal`. La clase `Perro` sobrescribe el método `hacerSonido` para representar el sonido específico de un perro. En el método `main`, creamos una instancia de la clase `Perro` y llamamos al método `hacerSonido` para imprimir el sonido del perro.
```java
class Animal {
    // Campo de la clase Animal
    protected String color;

    // Método de la clase Animal
    public void hacerSonido() {
        System.out.println("El animal hace un sonido genérico.");
    }
}

class Perro extends Animal {
    // Método de la clase Perro que sobrescribe el método de la clase Animal
    @Override
    public void hacerSonido() {
        System.out.println("El perro dice ¡Guau! ¡Guau! y es de color " + color); 
    }

}

public class Main {
    public static void main(String[] args) {
        Perro miPerro = new Perro();

        // Accediendo al campo tipo heredado de la clase Animal
        miPerro.color = "Marrón";

        // Accediendo al método hacerSonido() heredado de la clase Animal
        miPerro.hacerSonido();

    }
}
```
Y vemos como el color del animal se hereda en la clase perro:
![[Pasted image 20240318201710.png]]
## EXTENDS
La palabra clave `extends` se utiliza para establecer una relación de herencia entre dos clases:
![[Pasted image 20240318201733.png]]
Este sería el resultado:
![[Pasted image 20240318201750.png]]
## ANOTACIÓN @OVERRIDE
  
La anotación `@Override` en Java se utiliza para indicar que un método en una subclase está sobrescribiendo un método de la superclase. Esto ayuda a mejorar la legibilidad y claridad del código.

---------

En este ejemplo, la clase `Perro` hereda de la clase `Animal` y sobrescribe el método `comer()` para personalizar el comportamiento para los perros. La anotación `@Override` se utiliza antes del método `comer()` en la clase `Perro`, lo que indica que estamos sobrescribiendo el método `comer()` de la clase padre `Animal`.
```java
class Animal {
    public void comer() {
        System.out.println("El animal está comiendo...");
    }
}

class Perro extends Animal {
    @Override
    public void comer() {
        System.out.println("El perro está comiendo croquetas.");
    }
}

public class Main {
    public static void main(String[] args) {
        Perro miPerro = new Perro();
        miPerro.comer(); // Llama al método comer() de la subclase Perro
    }
}
```
![[Pasted image 20240318201043.png]]
## PROTECTED
`protected`, significa que ese miembro es accesible dentro del mismo paquete y también por todas las subclases:
![[Pasted image 20240318201945.png]]
Por lo tanto, `protected` proporciona un nivel de encapsulación que permite un cierto grado de acceso a los miembros de la clase desde las subclases, mientras que aún se mantiene la encapsulación y la seguridad de los datos dentro del objeto.
