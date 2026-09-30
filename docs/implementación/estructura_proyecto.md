---
id: estructura_proyecto
title: Estructura del Proyecto
sidebar_label: Estructura del Proyecto
---

# Implementación: Estructura del Proyecto

En esta sección se describe cómo está organizado el código fuente de **TaskFlow**.

## 1. Estructura general de carpetas

```text
taskflow/
├── backend/
│   ├── src/
│   │   ├── controllers/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── services/
│   │   ├── middlewares/
│   │   └── index.ts
│   ├── tests/
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── hooks/
│   │   ├── services/
│   │   └── App.tsx
│   ├── public/
│   └── package.json
├── docs/
├── .github/workflows/
└── README.md
```

## 2. Descripción de módulos

### Backend
| Carpeta | Responsabilidad |
|---------|-----------------|
| `controllers/` | Gestión de peticiones HTTP |
| `models/` | Entidades y acceso a datos (ORM) |
| `routes/` | Definición de endpoints REST |
| `services/` | Lógica de negocio |
| `middlewares/` | Autenticación, validación, errores |

### Frontend
| Carpeta | Responsabilidad |
|---------|-----------------|
| `components/` | Componentes reutilizables (botones, tarjetas, modales) |
| `pages/` | Vistas asociadas a rutas |
| `hooks/` | Custom hooks (useAuth, useTasks) |
| `services/` | Cliente HTTP y lógica de acceso a API |

## 3. Convenciones de código

- **Lenguaje:** TypeScript en frontend y backend.
- **Nombres:** `camelCase` para variables y funciones, `PascalCase` para clases y componentes.
- **Formato:** Prettier + ESLint con reglas compartidas.
- **Commits:** Conventional Commits (`feat:`, `fix:`, `docs:`...).

## 4. Ejemplo de endpoint REST

```http
POST /api/tasks
Authorization: Bearer <token>
Content-Type: application/json

{
  "titulo": "Diseñar login",
  "descripcion": "Crear pantalla de login",
  "prioridad": "ALTA",
  "fechaLimite": "2025-06-30"
}
```

Respuesta:

```json
{
  "id": "b1e2...",
  "titulo": "Diseñar login",
  "estado": "POR_HACER",
  "creadaEn": "2025-06-01T10:00:00Z"
}
```

## 5. Scripts disponibles

| Comando | Descripción |
|---------|-------------|
| `npm run dev` | Inicia el servidor en desarrollo |
| `npm run build` | Compila el proyecto |
| `npm run test` | Ejecuta las pruebas |
| `npm run lint` | Analiza el código con ESLint |

