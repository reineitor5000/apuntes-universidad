# Patrones de Diseño de Software Orientado a Objetos

## 1. Conceptos Básicos
Los patrones de diseño proporcionan catálogos de elementos reusables en el diseño de software. Su objetivo es evitar la reiteración en la búsqueda de soluciones a problemas ya conocidos, formalizar un vocabulario común entre diseñadores y estandarizar el diseño.

**Tipos según el dominio:**
* **Independientes de dominio:** Generales, aplicables a cualquier aplicación (ej. Patrones GoF - Gang of Four).
* **Específicos del dominio:** Diseñados para un tipo particular de entorno (aplicaciones bancarias, médicas, etc.).

**Elementos básicos de un patrón:**
1. **Contexto:** Situación en la que se presenta el problema.
2. **Problema:** Descripción del problema a resolver.
3. **Solución:** Medidas a tomar (crear clases, atributos, métodos, comportamientos).

## 2. Clasificación de los Patrones
Se dividen en tres grandes grupos:

### A. Creacionales
Se centran en cómo crear objetos de manera flexible y controlada. Abordan la complejidad en la creación de objetos y ocultan detalles de implementación cuando el uso directo de `new` no es conveniente.
* **Patrones:** Abstract Factory, Builder, Factory Method, Prototype, Singleton.

### B. Estructurales
Se enfocan en cómo componer objetos y clases para formar estructuras flexibles respetando el bajo acoplamiento. Ayudan a adaptar interfaces incompatibles o añadir comportamiento sin modificar el código existente.
* *Nota:* Para bajo acoplamiento, se prefiere la composición de clases por encima de la herencia.
* **Patrones:** Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy.

### C. Comportamentales
Se centran en cómo los objetos interactúan entre sí, cómo se reparten las responsabilidades y cómo se comunican de manera efectiva.
* **Patrones:** Chain of Responsibility, Command, Interpreter, Iterator, Mediator, Memento, Observer, State, Strategy, Template Method, Visitor.

---

## 3. Patrón Singleton (Creacional)
**Propósito:** Restringir la creación de objetos, garantizando que una clase tenga una única instancia, y proporcionar un punto de acceso global a ella.

**Contexto y Usos:**
Cuando se necesita exactamente una instancia para coordinar acciones en todo el sistema. Ejemplos: 
* Conexiones a bases de datos.
* Loggers.
* Administrador de ventanas.
* Objetos de configuración.
* *Nota:* Todos los componentes de negocio en Spring son Singleton por defecto.

**Implementación (Diagrama UML):**
1. Ocultar el constructor haciéndolo **privado** (`- Singleton()`).
2. Crear una variable de instancia **estática y privada** de la misma clase (`- instance: Singleton`).
3. Proporcionar un método **público y estático** que devuelva esa única instancia (`+ getInstance(): Singleton`).

**Consecuencias:**
* *Positivas:* Control de acceso estricto, reduce uso de recursos compartidos.
* *Negativas:* Difícil de testear (oculta dependencias), genera acoplamiento global, problemas de concurrencia.

**Problemas en Multihilo (Multi-thread):**
En un ambiente de un solo hilo, la implementación básica (`if instance == null { instance = new Singleton() }`) funciona. Sin embargo, en ambientes multihilo, si dos hilos evalúan el `null` al mismo tiempo, se pueden crear múltiples instancias. Es necesario colocar un bloqueo de hilo (sincronización) en la evaluación.