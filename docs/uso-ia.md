# RiojaReporta — Uso de inteligencia artificial

El profesor pidió documentar el uso de IA durante el desarrollo: herramientas, agentes y tokens consumidos. Este documento define **qué herramientas usamos, qué proveedores son de confianza y cómo se registra el consumo**.

## 1. Herramientas

- **OpenCode**, configurado para enviar todos los pedidos a través de **OmniRoute**.
- OmniRoute comprime los pedidos y registra el consumo de cada uno (tokens de entrada, de salida y ahorrados por compresión).
- **Todos deben usar la misma configuración.** Lo que no pasa por OmniRoute no queda registrado.

## 2. Proveedores de confianza

El criterio es qué hace cada proveedor con el código que le enviamos: si lo usa para entrenar sus modelos o lo pueden leer personas.

### Recomendados

| Proveedor | Qué dicen sus condiciones | Fuente |
|---|---|---|
| Anthropic (API de Claude) | No usa las entradas ni las salidas de la API para entrenar, salvo que el cliente lo acepte o envíe comentarios | [Anthropic](https://support.anthropic.com/en/articles/7996868-is-my-data-used-for-model-training) |
| OpenAI (API) | No usa los datos de la API para entrenar por defecto; los conserva hasta 30 días para control de abuso | [Meetily](https://meetily.ai/llm-privacy/openai) |
| Google Gemini (API **de pago**) | El contenido no se usa para mejorar sus productos | [Meetily](https://meetily.ai/llm-privacy/gemini) |

### Usar con precaución

| Proveedor | Motivo |
|---|---|
| Google Gemini (API **gratuita**) | El contenido puede usarse para mejorar los productos de Google y puede ser revisado por personas ([AMPM](https://ampm-aiops.com/en/guides/gemini-free-tier-data-tradeoff-2026/)) |
| Modelos gratuitos de otros proveedores | Cada uno tiene su propia política, y muchos no la publican con claridad |

### Regla general

- **Si no encontrás por escrito que el proveedor no entrena con los datos de la API, tratalo como "usar con precaución".**
- El código de RiojaReporta no es confidencial, así que los proveedores "con precaución" se pueden usar para programar.
- **Nunca, con ningún proveedor**, se envían:
  - el archivo `.env` ni ninguna clave, contraseña o token;
  - datos personales reales de vecinos (nombres, correos, direcciones particulares, fotos reales).

> Las políticas de los proveedores cambian. Esta tabla se revisó el 25/11/2026 con fuentes secundarias; ante una duda, consultar la página oficial del proveedor.

## 3. Registro de consumo

Cada integrante registra su consumo **en cada pull request**, en la sección "Uso de IA" de la plantilla del PR. Los datos salen del historial de uso de OmniRoute, filtrando por el período en que trabajó en esa tarea.

| Campo | Ejemplo |
|---|---|
| Tarea / PR | #12 — Registro de reclamos con fotos |
| Integrante | Kevin |
| Modelos usados | Claude Sonnet, Gemini Flash |
| Tokens de entrada | 184.000 |
| Tokens de salida | 22.500 |
| Tokens ahorrados por compresión | 41.000 |
| Para qué se usó | Generar el formulario en pasos y los tests de `validarFotos` |
| Qué se corrigió a mano | La validación de cantidad de fotos permitía 4 |

El último campo es el más importante para el informe: muestra **qué hizo la IA y qué tuvieron que corregir ustedes**.

## 4. Totales para el informe

Al cerrar cada semana, Uriel (líder de la base técnica) suma los consumos registrados en los PR de esa semana en la tabla de abajo.

| Semana | Tokens de entrada | Tokens de salida | Tokens ahorrados | PR incluidos |
|---|---|---|---|---|
| | | | | |
