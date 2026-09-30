---
id: requisitos
title: Análisis de Requisitos
sidebar_label: Requisitos
sidebar_position: 2
---

# Análisis de Requisitos

En esta sección se recogen los requisitos del sistema **TaskFlow**, clasificados en funcionales y no funcionales.

## 1. Requisitos funcionales (RF)

| ID | Descripción | Prioridad |
|----|-------------|-----------|
| RF-01 | El sistema permitirá registrar usuarios con email y contraseña. | Alta |
| RF-02 | El usuario podrá iniciar y cerrar sesión de forma segura. | Alta |
| RF-03 | El usuario podrá crear, editar y eliminar tareas. | Alta |
| RF-04 | Cada tarea tendrá: título, descripción, estado, prioridad y fecha límite. | Alta |
| RF-05 | El usuario podrá asignar tareas a otros miembros del equipo. | Media |
| RF-06 | El sistema mostrará un tablero Kanban con columnas: *Por hacer*, *En progreso*, *Hecho*. | Alta |
| RF-07 | El usuario podrá arrastrar tareas entre columnas. | Media |
| RF-08 | El sistema enviará notificaciones por email ante asignaciones. | Baja |
| RF-09 | El usuario podrá filtrar tareas por prioridad y responsable. | Media |
| RF-10 | El sistema generará un reporte semanal de tareas completadas. | Baja |

## 2. Requisitos no funcionales (RNF)

| ID | Descripción | Categoría |
|----|-------------|-----------|
| RNF-01 | El sistema debe responder en menos de 2 segundos en operaciones comunes. | Rendimiento |
| RNF-02 | La contraseña se almacenará con hash bcrypt (coste ≥ 10). | Seguridad |
| RNF-03 | La interfaz debe ser responsive (móvil, tablet, escritorio). | Usabilidad |
| RNF-04 | El sistema debe soportar al menos 100 usuarios concurrentes. | Escalabilidad |
| RNF-05 | El código debe tener una cobertura de pruebas ≥ 80 %. | Calidad |
| RNF-06 | El sistema debe ser accesible según WCAG 2.1 nivel AA. | Accesibilidad |

## 3. Casos de uso principales

### CU-01: Crear tarea

- **Actor:** Usuario autenticado
- **Precondición:** Sesión iniciada
- **Flujo principal:**
  1. El usuario pulsa "Nueva tarea".
  2. Rellena el formulario.
  3. El sistema valida los datos.
  4. La tarea se guarda y aparece en el tablero.

### CU-02: Mover tarea

- **Actor:** Usuario autenticado
- **Flujo principal:**
  1. El usuario arrastra una tarjeta.
  2. El sistema actualiza el estado.
  3. Se registra el cambio en el historial.

## 4. Restricciones

- La aplicación debe funcionar en navegadores modernos (Chrome, Firefox, Edge, Safari).
- El backend se desplegará en un entorno con Node.js 20 LTS.
- El presupuesto de infraestructura mensual no debe superar los 50 €.
