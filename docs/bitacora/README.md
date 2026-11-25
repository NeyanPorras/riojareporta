# Bitácora de problemas

Cada problema relevante que aparezca durante el desarrollo se registra acá: un archivo por problema, con el nombre `AAAA-MM-DD-descripcion-corta.md` (por ejemplo, `2026-11-28-fotos-superan-1mb.md`).

**¿Qué se registra?** Todo lo que haya costado más de 30 minutos resolver, que haya roto algo de otro módulo o que haya obligado a cambiar una decisión de diseño. Los errores de tipeo no.

**¿Cuándo?** Al resolverlo, no al final del proyecto. El pull request que lo soluciona enlaza el archivo de la bitácora.

## Plantilla

Copiar este bloque en el archivo nuevo:

```markdown
# Título breve del problema

- **Fecha:** AAAA-MM-DD
- **Integrante:** 
- **Módulo:** auth / reclamos / mapa / gestion / base técnica
- **Pull request:** #

## Qué pasó
Qué se intentaba hacer y qué ocurrió en su lugar. Incluir el mensaje de error, si lo hubo.

## Causa
Por qué pasaba.

## Solución
Qué se cambió para resolverlo.

## ¿Intervino la IA?
Si el problema lo generó o lo resolvió la IA, contarlo y explicar qué hubo que corregir.
```
