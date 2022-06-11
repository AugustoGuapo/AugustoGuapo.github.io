---
layout: post
title: Como hacer un login con netbeans
subtitle: sin morir en el intento

---

Para este tutorial asumiré que eres un compañero de mi clase de programación I en la U, así que no me detendré a explicar las bases de lo siguiente que aparecerá aquí. Si aún después de seguir todos los pasos, el programa no te funciona, siéntete libre de guardarte tus preguntas, estoy haciendo esto para que no me escriban.

Ahora sí, comienza la explicación.

## ¿Qué es lo primero?

Crearemos un nuevo proyecto en NetBeans, no importa la versión que uses, el procedimiento es el mismo. Luego de haber creado las 3 clases que asumo ya sabes hacer para el modelo-vista-controlador, empezamos.

### Clase modelo

En esta clase declaramos dos arreglos, uno para los usuarios y otro para las contraseñas, en este caso utilizaremos estos arreglos para almacenar estos datos de forma paralela, por lo que la contraseña correspondiente a un usuario será la que se encuentre en su misma posición. Yo utilicé los siguientes pero tu puedes hacer tus arreglos personales para probar.
```java
private String[] usuarios = {"admin", "noadmin"};
private String[] contraseñas = {"admin", "123456"};
```
Luego, basándonos en la teoría anterior, y utilizando los arreglos que creamos diseñaremos dos funciones para comprobar si el inicio de sesión fue correcto. 

Lo primero es conseguir la posición del usuario, para lo que usamos la siguiente función.
```java
public int verificarPosicionUsuario(String nombre) { //recibe el nombre del usuario
    int posicion =-1;
    for (int i = 0; i<usuarios.length; i++) {
        if(usuarios[i].equals(nombre)) { //compara el nombre ingresado con los del arreglo 
            posicion=i;//si alguno coincide guarda el valor
            break;
        }
    }
    return posicion;//En caso de que no coincida nunca, devuelve -1, de lo contrario devuelve la posición.
}
``` 
La siguiente función será de tipo booleano y verificará si la contraseña es correcta para el nombre de usuario.

```java
public boolean verificarClave(String nombre, String contraseña) {
    boolean resultado;
    int posicionUsuario = verificarPosicionUsuario(nombre);
    if(posicionUsuario>=0)
        resultado = contraseña.equals(contraseñas[posicionUsuario]);
    else
        resultado= false;
    return resultado; 
}
```
Como ven esta función recibe dos parámetros, nombre y contraseña, lo que hace es buscar la posición de este usuario en el arreglo, en caso de que este número sea -1, asigna y devuelve false, de lo contrario realiza la comparación de la contraseña introducida con la guardada en el arreglo y asigna el valor según sea el caso.

### Clase vista

En el JFrame utilizaremos los siguientes elementos:

* jTextField: Elemento básico para la entrada de datos por teclado
* jPasswordField: Básicamente lo mismo que el anterior pero no puedes ver lo que escribes, y la extracción de datos es un poco distinta.
* jLabel: Etiqueta simple para nombrar elementos en la interfaz, no tendrán utilidad más allá de la estética en este proyecto.
* jButton: Es un botón.
  
Yo procedí a colocarlos de la siguiente forma:

![Muestra de la ventana](https://i.imgur.com/6RlxTLV.png "¿pa qué colocas el mouse aquí?")

Como ya pueden sospechar, en esta clase crearemos un objeto de la clase que previamente programamos para el manejo de los arreglos, y para el botón utilizaremos lo siguiente

```java
private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         
    String contraseña = String.valueOf(jPasswordField1.getPassword()); //getPassword() devuelve un arreglo de char, para convertirlo en string utilizamos valueOf() de la clase String.
    String nombre = jTextField1.getText();
    
    if (obj.verificarClave(nombre, contraseña)) 
        JOptionPane.showMessageDialog(rootPane, "Inicio de sesión exitoso");
    else
        JOptionPane.showMessageDialog(rootPane, "Usuario o contraseña inválida"); 
} 
```

Y esto sería todo, espero seriamente que esta guía les haya sido de ayuda, espero que tengan buen día y 0 bugs. ¡Hasta la próxima!.