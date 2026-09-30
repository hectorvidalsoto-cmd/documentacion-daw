---
id: diagrama_clases
title: Diagrama de Clases
sidebar_label: Diagrama de Clases
sidebar_position: 3
---

# Diseño: Diagrama de Clases

El modelo de dominio de **TaskFlow** se representa mediante el siguiente diagrama de clases UML.

## 1. Diagrama general

```mermaid
classDiagram
    class Usuario {
        +UUID id
        +String nombre
        +String email
        +String passwordHash
        +Rol rol
        +login()
        +logout()
        +crearTarea()
    }

    class Tarea {
        +UUID id
        +String titulo
        +String descripcion
        +Estado estado
        +Prioridad prioridad
        +Date fechaLimite
        +cambiarEstado()
        +asignar()
    }

    class Tablero {
        +UUID id
        +String nombre
        +List~Tarea~ tareas
        +agregarTarea()
        +filtrar()
    }

    class Proyecto {
        +UUID id
        +String nombre
        +List~Usuario~ miembros
        +List~Tablero~ tableros
        +invitarUsuario()
    }

    class Notificacion {
        +UUID id
        +String mensaje
        +Date fecha
        +enviar()
    }

    class Rol {
        <<enumeration>>
        ADMIN
        MIEMBRO
        INVITADO
    }

    class Estado {
        <<enumeration>>
        POR_HACER
        EN_PROGRESO
        HECHO
    }

    class Prioridad {
        <<enumeration>>
        BAJA
        MEDIA
        ALTA
    }

    Usuario "1" -- "0..*" Tarea : asignada
    Usuario "1" -- "0..*" Proyecto : participa
    Proyecto "1" *-- "1..*" Tablero : contiene
    Tablero "1" *-- "0..*" Tarea : agrupa
    Usuario "1" -- "0..*" Notificacion : recibe
    Usuario --> Rol
    Tarea --> Estado
    Tarea --> Prioridad
```

## 2. Descripción de las clases

### Usuario

Representa a una persona registrada. Contiene credenciales y un rol que determina sus permisos.

### Tarea

Unidad mínima de trabajo. Su ciclo de vida está controlado por el enum `Estado`.

### Tablero

Agrupación visual de tareas tipo Kanban. Cada proyecto puede tener varios tableros.

### Proyecto

Contenedor de nivel superior. Agrupa usuarios y tableros.

### Notificacion

Mensajes generados ante eventos relevantes (asignaciones, cambios de estado).

## 3. Relaciones clave

- **Usuario – Tarea:** 1 a N (un usuario puede tener muchas tareas asignadas).
- **Proyecto – Tablero:** composición (los tableros no existen sin proyecto).
- **Tablero – Tarea:** composición (las tareas pertenecen a un tablero).
- **Usuario – Proyecto:** muchos a muchos (representado con lista).

## 4. Patrones de diseño aplicados

| Patrón | Aplicación |
|--------|------------|
| Repository | Acceso a datos desacoplado de la lógica de negocio |
| Observer | Notificaciones ante cambios de estado |
| DTO | Transferencia de datos entre frontend y backend |
| Factory | Creación de tareas según tipo (normal, recurrente) |
