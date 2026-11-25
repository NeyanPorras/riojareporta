# RiojaReporta — División de tareas

> Estado: **aprobado por el grupo** (25/11/2026).
> Los tiempos son **estimativos**: indican cuántos días de trabajo debería llevar cada tarea, no una fecha de entrega. Sirven para que cada uno sepa si va bien o si se trabó y conviene pedir ayuda.

## Cómo se trabaja cada tarea

1. Crear una rama desde `main` con el nombre `tipo/modulo-descripcion`. Por ejemplo, `feat/reclamos-mis-reclamos`.
2. Programar dentro de la carpeta del propio módulo, siguiendo [arquitectura.md](arquitectura.md).
3. Correr los tests (`npm test`) antes de subir.
4. Abrir un pull request completando la plantilla: qué hace, cómo se probó, problemas encontrados y uso de IA.
5. Esperar la aprobación de otro integrante. Recién ahí se hace el merge.

**Una tarea está terminada cuando** cumple su criterio de terminado, sus tests pasan, el PR tiene la plantilla completa y fue aprobado.

## Orden general

```
T1 Proyecto base ─┬─ T2 Base de datos ─┬─ módulos (reclamos, mapa, gestión)
                  │                    │
                  └─ T6 Ingreso ───────┴─ T7 Roles ── pantallas con permisos
```

- **T1 y T2 de Uriel van primero:** todo el resto los necesita.
- Mientras tanto, los demás pueden avanzar con sus `rules.ts` y sus tests, que no dependen de la base de datos ni de las pantallas.

## Uriel — Base técnica y autenticación

| # | Tarea | Días | Depende de | Terminado cuando |
|---|---|---|---|---|
| T1 | Crear el proyecto Next.js con TypeScript, Tailwind CSS y shadcn/ui, con la estructura de carpetas de la arquitectura | 1 | — | `npm run dev` levanta la app y las carpetas `modules/` y `shared/` existen |
| T2 | Configurar PostgreSQL con PostGIS en Docker, conectar Drizzle y crear el esquema completo del DER con su primera migración | 2 | T1 | `docker compose up` y la migración crean todas las tablas; hay datos iniciales de áreas y categorías |
| T3 | Configurar Vitest y el comando `npm test` | 0,5 | T1 | `npm test` corre un test de ejemplo |
| T4 | Almacenamiento de imágenes: función que entrega la URL temporal de subida (`shared/storage`) | 1,5 | T1 | Una foto de prueba se sube y queda accesible por su enlace |
| T5 | Configurar la aplicación web progresiva: manifiesto y service worker | 1 | T1 | La app se puede instalar en un celular |
| T6 | Configurar Better Auth con Google y correo electrónico, y armar la pantalla 1, Ingreso | 2 | T2 | Se puede ingresar con Google y con correo |
| T7 | Roles: `requerirSesion`, `requerirRol` y redirección según el rol al ingresar | 1 | T6 | Un vecino va al mapa; un operador, a la bandeja; un vecino no puede ejecutar acciones de operador |
| T8 | Pantalla 7, Perfil, con cierre de sesión | 0,5 | T6 | Muestra los datos del usuario y cierra la sesión |
| | **Total** | **9,5** | | |

## Kevin — Reclamos

| # | Tarea | Días | Depende de | Terminado cuando |
|---|---|---|---|---|
| T9 | Reglas en `rules.ts`: `validarFotos` (de 1 a 3, tipo y tamaño) y `puedeAnular` (solo en estado Recibido), con sus tests | 1 | T3 | Los tests cubren cada caso permitido y rechazado |
| T10 | Pantalla 4, Nuevo reclamo: pasos de categoría, fotos (con compresión y subida), descripción y confirmación, más la acción `crearReclamo` | 4 | T2, T4, T7, T9 | Un vecino crea un reclamo con fotos y se guarda en estado Recibido |
| T11 | Paso 3 de la pantalla 4: ubicación por GPS con el pin ajustable, usando el mapa base de Nella | 1,5 | T10, T14 | El reclamo guarda la ubicación elegida |
| T12 | Pantalla 5, Mis reclamos | 1 | T10 | Lista solo los reclamos del vecino, con su estado |
| T13 | Pantalla 6, Detalle de mi reclamo, con historial y anulación | 1,5 | T12 | Se puede anular en estado Recibido y en ningún otro |
| | **Total** | **9** | | |

## Nella — Mapa público y adhesiones

| # | Tarea | Días | Depende de | Terminado cuando |
|---|---|---|---|---|
| T14 | Componente base de mapa con MapLibre, en `shared/ui`. Lo usan las pantallas 2, 4 y 9 | 1,5 | T1 | El mapa se muestra centrado en la ciudad de La Rioja y permite marcar puntos |
| T15 | Pantalla 2, Mapa, con los reclamos y el filtro por categoría | 2 | T2, T14 | Se ven los reclamos de todos los vecinos y el filtro funciona |
| T16 | Pantalla 3, Detalle de reclamo, con el botón "Yo también" y la regla "un vecino adhiere una sola vez", con sus tests | 2 | T15 | La adhesión se guarda una vez por vecino y el contador se actualiza |
| T17 | Consulta de reclamos cercanos con PostGIS y aviso en el paso 3 del nuevo reclamo, expuesto a Kevin por `mapa/index.ts` | 2 | T2, T16 | Al marcar un punto a menos de la distancia definida de un reclamo de la misma categoría, aparece el aviso |
| | **Total** | **7,5** | | |

## Victor — Gestión municipal

| # | Tarea | Días | Depende de | Terminado cuando |
|---|---|---|---|---|
| T18 | Reglas en `rules.ts`: qué cambios de estado se permiten (por ejemplo, un reclamo Resuelto no vuelve a Recibido), con sus tests | 1 | T3 | Los tests cubren cada transición permitida y rechazada |
| T19 | Pantalla 8, Bandeja del área: tabla, filtros, orden por adhesiones y buscador por dirección | 2,5 | T2, T7 | Un operador ve solo los reclamos de su área |
| T20 | Pantalla 9, Gestión de reclamo: detalle, cambio de estado con observación y registro en el historial | 2,5 | T18, T19 | Cada cambio queda en el historial con el operador y la fecha |
| T21 | Pantalla 10, Administración: alta, edición y baja de categorías, áreas y operadores | 3 | T7 | Solo un administrador entra y puede gestionar los tres tipos de datos |
| | **Total** | **9** | | |

## Todos — Cierre

| # | Tarea | Días | Depende de | Terminado cuando |
|---|---|---|---|---|
| T22 | Integración y prueba completa del recorrido: un vecino crea un reclamo, otro adhiere y un operador lo resuelve | 2 | Todas las anteriores | El recorrido completo funciona sin errores |
| T23 | Manual de usuario: cada integrante redacta la sección de sus pantallas | 1 | T22 | El manual cubre las 10 pantallas |

## Decisiones pendientes antes de empezar

| Decisión | La necesita | Por qué |
|---|---|---|
| Servicio de almacenamiento de imágenes | T4 | Hay que elegir dónde se guardan las fotos |
| Proveedor de mapas vectoriales | T14 | MapLibre necesita una fuente de mapas |
| Distancia para considerar un reclamo "cercano" | T17 | Por ejemplo, 30 metros |
