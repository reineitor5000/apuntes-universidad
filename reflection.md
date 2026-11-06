# Reflection (Reflexión) en Java

## ¿Qué es Reflection?
En Java, Reflection es una API que permite examinar y utilizar clases, interfaces, campos, métodos y constructores en **tiempo de ejecución**. Pertenece principalmente a los paquetes `java.lang` y `java.lang.reflect`.

A diferencia de la *introspección* (que solo consulta características como "¿de qué tipo es este objeto?"), Reflection permite **operar dinámicamente** sobre esos miembros: inspeccionar metadatos, manipular atributos privados y crear instancias dinámicamente utilizando únicamente cadenas de texto (Strings).

## Ejemplo de Uso: Instanciación Dinámica
El siguiente código muestra cómo usar Reflection para implementar un patrón Factory dinámico basado en una configuración (ej. un archivo `config.properties`).

```java
package com;

import com.inter.UIFactory;
import com.inter.Ventana;
import com.inter.Boton;

public class Principal {
    public static void main(String[] args) {
        try {
            // 1. Obtener el valor de configuración (simulando lectura de config.properties)
            String tema = "oscuro"; 
            
            // 2. Construir el nombre completo del paquete y clase dinámicamente
            // Resultado: "com.impl.UIFactoryOscuro"
            String nombreClase = "com.impl.UIFactory" + 
                                 tema.substring(0, 1).toUpperCase() + 
                                 tema.substring(1);

            // 3. Buscar la clase en tiempo de ejecución usando Reflection
            Class<?> tipo = Class.forName(nombreClase);

            // 4. Crear la instancia dinámicamente y hacer cast a la interfaz común
            UIFactory factory = (UIFactory) tipo.getDeclaredConstructor().newInstance();

            // 5. Utilizar los métodos de la fábrica sin acoplamiento a clases concretas
            Ventana ventana = factory.crearVentana();
            Boton boton = factory.crearBoton();

            ventana.abrir();
            boton.dibujar();

        } catch (Exception e) {
            // Manejo obligatorio de excepciones como ClassNotFoundException, 
            // NoSuchMethodException e InvocationTargetException
            e.printStackTrace();
        }
    }
}
```

## Explicación paso a paso
1. **Definición de variables:** Se arma el nombre exacto de la clase concatenando el texto configurado.
2. **`Class.forName()`:** Busca y carga la clase por su nombre dentro de la JVM, devolviendo el objeto `Class` asociado.
3. **`getDeclaredConstructor().newInstance()`:** 
   * `getDeclaredConstructor()` busca un constructor (incluso si tiene diferentes niveles de acceso).
   * `newInstance()` crea la instancia (en Java moderno, `Class.newInstance()` está obsoleto, se usa a través del constructor).
4. **Casting:** Se moldea el objeto a la interfaz común (`UIFactory`).
5. **Excepciones:** Al depender de textos, si la clase no existe o falla, Java lanzará excepciones que deben ser capturadas obligatoriamente.