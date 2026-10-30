# Actividad: Desarrollo de una interfaz gráfica para un RPG con Java Swing
Por equipos
Fecha entrega: 11 Noviembre 2026

## 1. Objetivo

Desarrollar una interfaz gráfica de usuario (GUI) utilizando Java Swing para interactuar con el sistema RPG implementado previamente.

La interfaz deberá permitir registrar personajes, consultar sus atributos, administrar sus inventarios y gestionar misiones mediante componentes gráficos y eventos.



## 2. Requisitos funcionales

### 2.1. Ventana principal

Crear una ventana principal utilizando `JFrame`.

La ventana deberá incluir:

- Título: RPG Character Manager.
- Un menú de navegación.
- Un área para mostrar la información del sistema.
- Una sección para administrar personajes.
- Una sección para consultar inventarios.
- Una sección para administrar misiones.

Se recomienda utilizar `JTabbedPane` para organizar las diferentes secciones.

### 2.2. Registro de personajes

Crear un formulario que permita registrar personajes.

El formulario deberá contener los siguientes componentes:

| Componente Swing | Función |
|---|---|
| `JTextField` | Introducir el nombre del personaje |
| `JComboBox` | Seleccionar el tipo de personaje |
| `JSpinner` | Introducir el nivel |
| `JSpinner` o `JTextField` | Introducir los puntos de salud |
| `JButton` | Registrar el personaje |
| `JButton` | Limpiar el formulario |
| `JTable` | Mostrar los personajes registrados |

Los tipos de personaje disponibles serán:

- Warrior
- Mage
- Archer
- Priest

Al registrar un personaje, el sistema deberá crear una instancia de la clase correspondiente.

Por ejemplo, si el usuario selecciona `Warrior`, se deberá crear un objeto de tipo `Warrior`, no un objeto genérico que solamente almacene el nombre del tipo.

**Requisito de POO:** todos los personajes deberán poder administrarse mediante referencias del tipo abstracto `Character`.

### 2.3. Consulta de personajes

El usuario deberá poder seleccionar un personaje de la tabla para consultar su información.

La aplicación deberá mostrar:

- Nombre.
- Tipo de personaje.
- Nivel.
- Puntos de salud.
- Estado: vivo o muerto.
- Información específica de su clase, cuando corresponda.

Por ejemplo, para un `Mage` se podrá mostrar el maná disponible, mientras que para un `Archer` se podrá mostrar la cantidad de flechas.

La interfaz deberá identificar el tipo concreto de personaje sin duplicar innecesariamente la lógica de combate o administración del modelo.

### 2.4. Administración del inventario

Crear una sección para consultar y administrar el inventario del personaje seleccionado.

La interfaz deberá permitir:

1. Seleccionar un personaje.
2. Consultar los objetos de su inventario.
3. Agregar un objeto.
4. Eliminar un objeto seleccionado.
5. Consultar el número de objetos almacenados.

Los objetos disponibles serán:

- Weapon
- Armor
- Potion
- Accessory
- Consumable

Para agregar un objeto, se deberá utilizar un formulario con campos apropiados para el tipo de objeto seleccionado.

Por ejemplo, una poción podrá tener un nombre, un valor de recuperación y un tipo de efecto.

El inventario deberá utilizar las clases del modelo y respetar su capacidad máxima, si esta regla se encuentra implementada.

Si una operación no puede realizarse, la interfaz deberá informar al usuario mediante un cuadro de diálogo.

### 2.5. Administración de misiones

Crear una sección para administrar las misiones del RPG.

La interfaz deberá permitir:

- Registrar una misión.
- Consultar las misiones existentes.
- Seleccionar una misión.
- Consultar sus participantes.
- Agregar personajes a una misión.
- Eliminar personajes de una misión.
- Consultar el estado de la misión.

El formulario de registro deberá contener, como mínimo:

| Campo | Componente sugerido |
|---|---|
| Nombre de la misión | `JTextField` |
| Descripción | `JTextArea` |
| Dificultad | `JComboBox` |
| Recompensa | `JSpinner` |
| Registrar misión | `JButton` |

Una misión podrá existir sin participantes. Asimismo, eliminar un personaje de una misión no deberá eliminar el objeto `Character` del sistema.

**Requisito de POO:** se deberá mantener la relación de agregación entre `Quest` y `Character`.

### 2.6. Manejo de errores

La aplicación deberá controlar las operaciones inválidas y mostrar mensajes comprensibles para el usuario.

Se deberán contemplar, como mínimo, los siguientes casos:

- Registrar un personaje sin nombre.
- Introducir un nivel o una cantidad de salud inválidos.
- Intentar agregar un objeto a un inventario lleno.
- Eliminar un objeto inexistente.
- Intentar atacar con un personaje muerto.
- Agregar un personaje duplicado a una misión.
- Intentar realizar una operación incompatible con el estado de una misión.

Cuando corresponda, se deberán utilizar las excepciones personalizadas desarrolladas en el proyecto RPG.

La interfaz deberá capturar las excepciones esperadas y mostrar sus mensajes mediante `JOptionPane`.

Ejemplo conceptual:

```java
try {
    // Ejecutar una operación del modelo.
} catch (InventoryFullException e) {
    JOptionPane.showMessageDialog(
        frame,
        e.getMessage(),
        "Inventario lleno",
        JOptionPane.WARNING_MESSAGE
    );
}
```

Este fragmento es ilustrativo. Deberá adaptarse a las clases y excepciones implementadas en el proyecto.


## 3. Arquitectura de la aplicación (Modelo Vista Controlador)

Se deberá separar la interfaz gráfica de las clases que representan el sistema RPG.

Se recomienda la siguiente organización lógica:

**Modelo**

Contiene las clases que representan los elementos del juego.

- `Character`
- `Warrior`
- `Mage`
- `Archer`
- `Priest`
- `Inventory`
- `Item`
- `Weapon`
- `Armor`
- `Potion`
- `Accessory`
- `Consumable`
- `Quest`

También incluye los repositorios genéricos y las excepciones personalizadas que se hayan implementado.

**Vista**

Contiene los componentes gráficos.

- `MainFrame`
- `CharacterPanel`
- `InventoryPanel`
- `QuestPanel`

**Controlador**

Contiene las clases responsables de coordinar las acciones de la interfaz con el modelo.

- `CharacterController`
- `InventoryController`
- `QuestController`

Los nombres anteriores son una propuesta de organización; se pueden adaptar a la estructura del proyecto existente.

## 4. Uso de programación genérica

Si el proyecto anterior incluye la clase `Repository<T>`, esta deberá utilizarse para administrar los elementos del sistema.

Por ejemplo:

- `Repository<Character>` para los personajes.
- `Repository<Item>` para los objetos.
- `Repository<Quest>` para las misiones.

Los controladores deberán interactuar con estos repositorios sin reemplazar los tipos genéricos por `Object`.

La tabla de personajes deberá obtener los datos de los objetos `Character` almacenados en el repositorio, mientras que la tabla de misiones deberá consultar los objetos `Quest`.

No es necesario que la interfaz gráfica implemente sus propias estructuras de almacenamiento si el modelo ya dispone de ellas.


## Entregables

El estudiante deberá entregar:

1. Código fuente completo del proyecto.

