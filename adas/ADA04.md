# Actividad: Desarrollo de una interfaz gráfica para un RPG con Java Swing

## 1. Objetivo

Desarrollar una interfaz gráfica de usuario (GUI) utilizando Java Swing para interactuar con el sistema RPG implementado previamente.

La interfaz deberá permitir registrar personajes, consultar sus atributos, administrar sus inventarios y gestionar misiones mediante componentes gráficos y eventos.

El estudiante deberá aplicar los conceptos de programación orientada a objetos y separar la lógica del sistema de la interfaz gráfica.

## 2. Descripción del problema

Se requiere desarrollar una aplicación de escritorio para administrar los personajes de un juego RPG.

Actualmente, el sistema permite crear personajes, administrar objetos y asignar misiones mediante código Java. Sin embargo, el usuario necesita interactuar con el sistema sin modificar el código fuente ni ejecutar instrucciones directamente desde la consola.

Para resolver este problema, se deberá construir una interfaz gráfica que permita realizar las operaciones principales del sistema mediante formularios, botones, listas y tablas.

La aplicación deberá utilizar las clases existentes del proyecto RPG, evitando duplicar en la interfaz la lógica de negocio correspondiente a los personajes, los inventarios y las misiones.

## 3. Requisitos funcionales

### 3.1. Ventana principal

Crear una ventana principal utilizando `JFrame`.

La ventana deberá incluir:

- Título: RPG Character Manager.
- Un menú de navegación.
- Un área para mostrar la información del sistema.
- Una sección para administrar personajes.
- Una sección para consultar inventarios.
- Una sección para administrar misiones.

Se recomienda utilizar `JTabbedPane` para organizar las diferentes secciones.

### 3.2. Registro de personajes

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

### 3.3. Consulta de personajes

El usuario deberá poder seleccionar un personaje de la tabla para consultar su información.

La aplicación deberá mostrar:

- Nombre.
- Tipo de personaje.
- Nivel.
- Puntos de salud.
- Estado: vivo o muerto.
- Información específica de su clase, cuando corresponda.

Por ejemplo, para un `Mage` se podrá mostrar el maná disponible, mientras que para un