# UML (Lenguaje de Modelado Unificado)

## 1. Introducción a UML
UML es un lenguaje gráfico que permite modelar, visualizar, especificar, construir y documentar los objetos de un sistema de software. Sirve principalmente para facilitar la transferencia de información y asegurar que todos los involucrados entiendan el diseño antes de escribir el código.

Se basa en tres principios fundamentales:
1. **Es un lenguaje.**
2. **Está unificado.**
3. **Permite modelar.**

## 2. Mecanismos de Extensibilidad y Metadatos
UML utiliza metadatos para transmitir información adicional o categorizar elementos.
* **Estereotipos (`<< >>`):** Son mecanismos que amplían el vocabulario de UML. Son "metatipos" que definen el propósito de un conjunto de elementos modelados. Ayudan a categorizar clases según su funcionalidad (ej. `<<Repository>>`, `<<interface>>`, `<<device>>`, `<<Exception>>`).
* **Restricciones:** Definen condiciones o reglas que se aplican a los elementos (perfiles o estereotipos). Se escriben en forma de nota y pueden ser restricciones de atributos o restricciones en relaciones (ej. `{edad >= 18}`).

## 3. Diagramas de Clases (Estructura Estática)
Es el diagrama principal para describir la estructura estática del sistema. Muestra clases, interfaces, objetos y sus relaciones.

### Elementos de una Clase
* **Atributos:** Representan propiedades de una entidad (datos primitivos o de referencia). Tienen un dominio de valores determinado.
* **Operaciones (Métodos):** Describen el comportamiento de los objetos de una clase.

### Visibilidad
* `+` Público (Public)
* `#` Protegido (Protected)
* `-` Privado (Private)
* `~` Por defecto (Default/Package)

### Relaciones entre Clases
Definen la conexión semántica entre los elementos:
1. **Asociación (Línea simple / Flecha):** Relación estructural donde un elemento conoce a otro. Define un rol y una multiplicidad.
2. **Agregación (Rombo hueco):** Relación de "todo y sus partes", pero las partes pueden existir independientemente del objeto complejo (ej. Equipo y Jugador).
3. **Composición (Rombo relleno):** Relación altamente dependiente. Si se elimina la clase principal, las entidades vinculadas a ella también se eliminan (ej. Factura y Detalles de Factura).
4. **Generalización / Herencia (Triángulo hueco):** Una clase genérica hereda sus atributos y métodos a clases específicas.
5. **Dependencia (Línea punteada):** Un cambio en una clase independiente requerirá cambios en la clase que depende de ella.

**Multiplicidad en Asociaciones:**
* `1` -> Sólo uno
* `0..1` -> Cero o uno
* `*` o `0..*` -> Cero o más
* `1..*` -> Uno o más

*Nota:* Existe la **Asociación Reflexiva**, que ocurre cuando una clase se relaciona consigo misma (ej. un Empleado que es jefe de otros Empleados).

## 4. Tipos de Modelos / Diagramas UML
* **Casos de Uso:** Estático (Análisis)
* **Clases:** Estático (Análisis y Diseño)
* **Objetos:** Estático (Análisis y Diseño). Muestra una "fotografía" o instancia específica en un momento dado.
* **Estados:** Dinámico (Análisis). Muestra los estados por los que pasa un objeto durante su vida debido a eventos.
* **Actividad:** Dinámico (Análisis)
* **Secuencia / Colaboración:** Dinámico (Diseño). Interacción cronológica de mensajes entre objetos.
* **Componentes / Despliegue:** Estático (Diseño). Organización física del sistema.

## Conceptos adicionales (Patrón Command en UML)
* **Invoker:** Solicita que se ejecute una acción.
* **Command:** Define la operación que se debe ejecutar.
* **ConcreteCommand:** Implementa la acción y conecta la solicitud.
* **Receiver:** Objeto que ejecuta el trabajo real.