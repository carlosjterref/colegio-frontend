# Colegio Yermo y Parres — Frontend

Cliente web del **Sistema de Información Académico** del Colegio Yermo y Parres.
Contiene el sitio institucional público y los portales privados por rol
(docentes, estudiantes, acudientes y administración).

> Este repositorio contiene **únicamente el frontend**.
> La API que consume está en [colegio-backend](https://github.com/carlosjterref/colegio-backend).

---

## Tecnologías

- **HTML5** y **CSS3**
- **JavaScript** (Vanilla, ES6+) — sin frameworks
- **Bootstrap 5.3** y **Bootstrap Icons** (vía CDN)

## Estructura

```
├── css/                # Hojas de estilo
│   ├── global.css          # Variables y estilos base
│   ├── home.css            # Sitio público
│   ├── components.css      # Sidebar, topbar, tarjetas y mensajes
│   └── ...                 # Estilos por vista
├── js/
│   ├── api.js              # Módulo central: consumo de la API, sesión y componentes compartidos
│   ├── docentes.js         # Dashboard del docente
│   ├── estudiantes.js      # Portal del estudiante
│   ├── acudientes.js       # Portal del acudiente
│   ├── admin.js            # Panel de administración
│   ├── micolegio.js        # Sitio público + consumo de API externa (festivos)
│   ├── plantel.js          # Plantel docente
│   ├── circulares.js       # Circulares
│   └── registro.js         # Registro de estudiante y acudiente
├── img/                # Recursos gráficos
└── *.html              # Páginas públicas, logins y portales
```

## Páginas

| Tipo | Archivos |
|------|----------|
| Públicas | `index.html`, `micolegio.html`, `plantel.html`, `circulares.html`, `contacto.html`, `Inscripcion.html`, `registro.html` |
| Autenticación | `login-docente.html`, `login-estudiantes.html`, `login-acudientes.html`, `login-admin.html` |
| Portales privados | `dashboard-docente.html`, `Portal-estudiante.html`, `Portal-acudiente.html`, `dashboard-admin.html` |

## Módulo `js/api.js`

Centraliza toda la comunicación con el servidor, evitando duplicar lógica en cada página:

- `apiFetch()` — peticiones a la API, adjuntando automáticamente el token JWT
- `login()`, `cerrarSesion()`, `exigirSesion()` — manejo de sesión y protección de vistas
- `cargarMensajesEn()`, `abrirMensaje()`, `responderMensaje()` — bandeja de mensajes compartida
- `cargarComunicadosEn()`, `cambiarContrasena()` — componentes reutilizables

La constante `API_URL` usa una **ruta relativa** (`/api`), por lo que funciona tanto en
desarrollo local como desplegado, siempre que el backend sirva estos archivos.

## Cómo ejecutarlo

El frontend **necesita el backend** para funcionar (login, notas, mensajes, etc.).

1. Clona y levanta el [backend](https://github.com/carlosjterref/colegio-backend).
2. Haz que el servidor Express sirva esta carpeta como contenido estático,
   o colócala como carpeta hermana del backend (`frontend/`), que es la disposición
   que espera `server.js` en el proyecto completo.
3. Abre <http://localhost:3000>.

> ⚠️ No abras los `.html` con doble clic (`file://`): las peticiones a la API fallarían.
> Debe servirse por HTTP desde el mismo origen que la API.

## Consumo de API externa

La sección **“Días Festivos”** de `micolegio.html` muestra los festivos de Colombia
obtenidos de la API pública [Nager.Date](https://date.nager.at), a través del
endpoint `/api/festivos` del backend.

## Repositorios relacionados

| Repositorio | Contenido |
|-------------|-----------|
| [proyecto-ficha83](https://github.com/carlosjterref/proyecto-ficha83) | Proyecto completo (frontend + backend) |
| [colegio-backend](https://github.com/carlosjterref/colegio-backend) | API REST / servidor |

---

**Autor:** Carlos Terreros — Proyecto Ficha 83
