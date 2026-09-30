---
id: github_pages
title: Despliegue en GitHub Pages
sidebar_label: GitHub Pages
---

# Despliegue: GitHub Pages

Esta sección describe cómo publicar la documentación de **TaskFlow** (y opcionalmente el frontend) en GitHub Pages.

## 1. Requisitos previos

- Repositorio en GitHub con la documentación en `/docs`.
- Node.js ≥ 18 instalado.
- Docusaurus configurado correctamente.

## 2. Configuración de Docusaurus

Edita `docusaurus.config.js`:

```javascript
module.exports = {
  title: 'TaskFlow Docs',
  url: 'https://tu-usuario.github.io',
  baseUrl: '/taskflow/',
  organizationName: 'tu-usuario',
  projectName: 'taskflow',
  trailingSlash: false,
  presets: [
    [
      'classic',
      {
        docs: { routeBasePath: '/' },
        blog: false,
      },
    ],
  ],
};
```

> **Importante:** `baseUrl` debe coincidir con el nombre del repositorio si no usas dominio propio.

## 3. Despliegue manual

```bash
# Instalar dependencias
npm install

# Compilar el sitio estático
npm run build

# Publicar en la rama gh-pages
GIT_USER=tu-usuario npm run deploy
```

## 4. Despliegue automático con GitHub Actions

Crea el archivo `.github/workflows/deploy.yml`:

```yaml
name: Deploy Docusaurus to GitHub Pages

on:
  push:
    branches: [main]

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 20

      - run: npm ci
      - run: npm run build

      - uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build
```

## 5. Activar GitHub Pages

1. Ve a **Settings → Pages**.
2. En *Source*, selecciona **Deploy from a branch**.
3. Elige la rama `gh-pages` y la carpeta `/ (root)`.
4. Guarda los cambios.

La web estará disponible en:

```text
https://tu-usuario.github.io/taskflow/
```

## 6. Dominio personalizado (opcional)

Crea un archivo `static/CNAME` con:

```text
docs.taskflow.example.com
```

Y configura en tu proveedor DNS un registro `CNAME` apuntando a `tu-usuario.github.io`.

## 7. Verificación

- Comprueba que la URL carga correctamente.
- Revisa que los enlaces relativos funcionan (`baseUrl` bien definido).
- Ejecuta `npm run serve` localmente para simular producción.

## 8. Solución de problemas comunes

| Problema | Causa probable | Solución |
|----------|----------------|----------|
| Página en blanco | `baseUrl` incorrecto | Ajustar al nombre del repo |
| CSS no carga | Rutas absolutas | Revisar `trailingSlash` |
| 404 en rutas | Falta `index.html` | Ejecutar `npm run build` |

