# RiojaReporta — Arquitectura base

> Estado: **aprobado por el grupo** (25/11/2026).

## 1. Organización por módulo funcional

El código se organiza por módulo de negocio, no por tipo de archivo. Cada integrante trabaja dentro de la carpeta de su módulo.

```
src/
  app/                      Rutas de Next.js. Solo arman la página y llaman a los módulos.
    (vecino)/               Mapa, detalle, nuevo reclamo, mis reclamos, perfil
    (municipal)/            Bandeja, gestión, administración
    api/auth/[...all]/      Única ruta de API: la que exige Better Auth
  modules/
    auth/        Uriel      Ingreso, sesión, roles y perfil
    reclamos/    Kevin      Alta de reclamos, mis reclamos, anulación
    mapa/        Nella      Mapa público, adhesiones, aviso de reclamos cercanos
    gestion/     Victor     Bandeja, cambio de estado, administración
  shared/
    db/                     Conexión y esquema de la base de datos
    auth/                   Configuración de Better Auth y control de roles
    storage/                Subida de fotos al almacenamiento
    ui/                     Componentes visuales comunes (shadcn/ui)
```

### Contenido de cada módulo

| Archivo | Qué contiene | Dónde se ejecuta |
|---|---|---|
| `components/` | Pantallas y componentes del módulo | Servidor o navegador |
| `queries.ts` | Lecturas de la base de datos | Solo servidor |
| `actions.ts` | Server Actions: validan, aplican reglas y escriben | Solo servidor |
| `rules.ts` | Reglas de negocio como funciones puras, sin base de datos ni pantalla | Cualquiera |
| `schema.ts` | Validación de los datos que llegan desde los formularios | Cualquiera |
| `index.ts` | Lo que el módulo expone a los demás | — |

## 2. Reglas de dependencia

- `app/` usa `modules/` y `shared/`.
- `modules/` usa `shared/`.
- `shared/` no usa ningún módulo.
- **Un módulo no importa archivos internos de otro.** Si necesita algo, lo toma del `index.ts` del otro módulo. Ejemplo: `mapa` usa la consulta de reclamos que expone `reclamos/index.ts`.
- Solo `queries.ts` y `actions.ts` acceden a la base de datos.

Estas reglas evitan que un cambio en un módulo rompa otro sin que nadie se entere.

## 3. Comunicación con el servidor

- **Leer:** las pantallas son Server Components que llaman a `queries.ts`.
- **Escribir:** los formularios llaman a Server Actions de `actions.ts`.
- **No hay API REST propia.** La única ruta de API es `app/api/auth/[...all]/route.ts`, que exige Better Auth.

### Flujo de una Server Action

1. Verificar sesión y rol del usuario.
2. Validar los datos con `schema.ts`.
3. Aplicar las reglas de `rules.ts` (por ejemplo, "solo se anula en estado Recibido").
4. Escribir en la base de datos.
5. Devolver el resultado a la pantalla.

### Fotos

Next.js limita a 1 MB por defecto lo que recibe una Server Action, y una foto de celular suele superar ese tamaño. Por eso:

1. El navegador comprime cada foto.
2. Una Server Action entrega una URL temporal de subida.
3. El navegador sube la foto directo al almacenamiento.
4. La Server Action que crea el reclamo recibe solo los enlaces de las fotos.

Todas las comprobaciones de fotos pasan por una única función, `validarFotos`, del módulo `reclamos`. Hoy verifica cantidad (1 a 3), tipo y tamaño. **Mejora futura:** analizar el contenido de las imágenes con un modelo de moderación, modificando solo esa función.

## 4. Base de datos

- **Esquema único en `shared/db/schema.ts`.** Las tablas son compartidas (la de reclamos la usan tres módulos), así que se definen en un solo lugar.
- **Cambios de esquema con migraciones** generadas por Drizzle. Nadie modifica la base de datos a mano.
- El esquema sigue el [diagrama entidad-relación](diagrama-entidad-relacion.png).

## 5. Autenticación y roles

- Better Auth se configura en `shared/auth/`.
- `shared/auth/` expone dos funciones que usan todos los módulos:
  - `requerirSesion()`: devuelve el usuario o lo envía al ingreso.
  - `requerirRol("operador" | "administrador")`: corta la acción si el usuario no tiene el rol.
- **Cada Server Action verifica el rol en el servidor.** Ocultar un botón en la pantalla no alcanza: cualquiera puede llamar a la acción igual.

## 6. Pruebas

- Las reglas de `rules.ts` se prueban con tests unitarios usando **Vitest**.
- Cada pull request incluye los tests de las reglas que agrega o modifica, y deben pasar antes de pedir revisión.

## Decisiones y alternativas descartadas

| # | Decisión | Alternativa descartada |
|---|---|---|
| 1 | Los módulos se comunican solo por su `index.ts` | Importar archivos internos de otros módulos: más rápido al principio, pero acopla los módulos |
| 2 | Esquema de base de datos único en `shared/db` | Un esquema por módulo: las tablas compartidas quedarían repartidas |
| 3 | Validación de formularios con **Zod** en `schema.ts` | Validar a mano en cada acción: repetitivo y propenso a errores |
| 4 | Control de roles centralizado en `shared/auth` | Que cada módulo verifique a su manera |
| 5 | Tests unitarios con **Vitest** | Jest: también funciona, pero requiere más configuración con TypeScript |
