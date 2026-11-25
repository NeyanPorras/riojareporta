# RiojaReporta — Pantallas

> Estado: **aprobado por el grupo** (25/11/2026). Los wireframes de cada pantalla están en [wireframes/wireframes.pdf](wireframes/wireframes.pdf).

## Vecino (celular)

| # | Pantalla | Qué contiene | Módulo |
|---|---|---|---|
| 1 | Ingreso | Botones "Entrar con Google" y "Entrar con correo" | M1 Uriel |
| 2 | Mapa (pantalla principal) | Mapa con los reclamos, filtro por categoría y botón "+ Nuevo reclamo" | M3 Nella |
| 3 | Detalle de reclamo | Fotos, categoría, estado, dirección, cantidad de adhesiones y botón "Yo también" | M3 Nella |
| 4 | Nuevo reclamo (en pasos) | 1. Categoría → 2. Fotos (1 a 3) → 3. Ubicación por GPS con pin ajustable y aviso si ya hay un reclamo cerca → 4. Descripción → 5. Confirmar | M2 Kevin (aviso: M3) |
| 5 | Mis reclamos | Lista de los reclamos propios con su estado | M2 Kevin |
| 6 | Detalle de mi reclamo | Igual que la 3, más el historial de estados y el botón "Anular" (solo en estado Recibido) | M2 Kevin |
| 7 | Perfil | Nombre, correo y cerrar sesión | M1 Uriel |

## Municipalidad (computadora)

| # | Pantalla | Qué contiene | Módulo |
|---|---|---|---|
| 8 | Bandeja del área | Tabla de reclamos del área, filtros por estado y categoría, orden por cantidad de adhesiones | M4 Victor |
| 9 | Gestión de reclamo | Fotos, ubicación en el mapa, historial y cambio de estado con observación (En proceso, Resuelto o Rechazado) | M4 Victor |
| 10 | Administración | Secciones para categorías, áreas y operadores (alta, edición y baja) | M4 Victor |

## Decisiones de diseño

- El mapa es la pantalla principal del vecino: primero ve lo que ya está reportado y después carga lo suyo.
- El aviso de reclamo cercano aparece en el paso 3 del nuevo reclamo, cuando ya se conoce la ubicación, para que el vecino pueda adherir en lugar de duplicar.
- Administración es una sola pantalla con tres secciones.
- El ingreso es el mismo para todos: según el rol, el usuario entra al mapa (vecino) o a la bandeja (operador o administrador).
