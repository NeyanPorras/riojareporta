# RiojaReporta

Aplicación web progresiva para que los vecinos de la ciudad de La Rioja reporten problemas de la vía pública (baches, fallas del alumbrado, basurales y árboles que requieren poda) con fotografías y ubicación, vean en un mapa los reclamos existentes y adhieran a ellos. La Municipalidad cuenta con un panel para gestionar y priorizar su atención.

Trabajo Final Integrador — Grupo 11 — Tecnicatura Universitaria en Programación, UTN Facultad Regional La Rioja.

## Equipo y módulos

| Integrante | Módulo |
|---|---|
| Uriel | Base técnica y autenticación (`modules/auth`) |
| Kevin | Reclamos (`modules/reclamos`) |
| Nella | Mapa público y adhesiones (`modules/mapa`) |
| Victor | Gestión municipal (`modules/gestion`) |

## Documentación

| Documento | Contenido |
|---|---|
| [División de tareas](docs/division-de-tareas.md) | Tareas de cada integrante, estimación, dependencias y criterio de terminado |
| [Arquitectura](docs/arquitectura.md) | Organización del código, comunicación con el servidor, base de datos, roles y pruebas |
| [Pantallas](docs/pantallas.md) y [wireframes](docs/wireframes/wireframes.pdf) | Las 10 pantallas aprobadas y su diseño de baja fidelidad |
| [Diagrama entidad-relación](docs/diagrama-entidad-relacion.png) | Estructura de la base de datos |
| [Uso de IA](docs/uso-ia.md) | Herramientas, proveedores de confianza y registro de consumo |
| [Bitácora de problemas](docs/bitacora/README.md) | Problemas encontrados y cómo se resolvieron |

## Tecnologías

TypeScript, Next.js, React, Tailwind CSS, shadcn/ui, PostgreSQL con PostGIS, Drizzle ORM, Better Auth, MapLibre GL JS, Zod, Vitest y Docker.

## Cómo trabajamos

1. Cada tarea se desarrolla en su propia rama, creada desde `main`.
2. Antes de subir los cambios, los tests tienen que pasar (`npm test`).
3. Se abre un pull request completando la plantilla, incluidas las secciones de problemas encontrados y uso de IA.
4. Otro integrante revisa y aprueba el pull request. Recién entonces se hace el merge.

## Estado

En desarrollo. La primera tarea es T1: crear el proyecto base (ver [División de tareas](docs/division-de-tareas.md)).
