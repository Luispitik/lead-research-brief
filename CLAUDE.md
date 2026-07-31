# CLAUDE.md — Lead Research Brief

Repositorio de la skill Lead Research Brief. `SKILL.md` es el fichero que Claude lee y
ejecuta; el resto es documentación o datos de soporte.

## Estructura

```
SKILL.md              Skill principal (6 fases, la 6ª opcional). Claude lee este fichero
README.md             Cara pública del repo: qué hace, qué no hace, instalación, ejemplo
LICENSE               CC BY-NC-SA 4.0
references/           Datos de soporte, leídos por fase
  research_vectors.md     Queries de búsqueda por sector (Fase 1)
  pain_library.md         Fricciones típicas por sector (Fases 2-3)
  html_template_guide.md  Especificación del HTML interactivo (Fase 4B)
  palette.md              Paleta y escalas categóricas (Fases 4B y 6)
  app_demo_guide.md       Guía de la demo-app (Fase 6)
```

## Cómo está pensado el diseño

- **Las referencias se leen por fase, no todas de golpe.** Cargarlas juntas gasta contexto
  que hace falta para la investigación. Si añades una referencia, di en `SKILL.md` en qué
  fase se lee.
- **El backlog (Fase 3) depende del mapa (Fase 2).** Cada módulo debe resolver al menos una
  fricción del mapa. Romper ese vínculo convierte el backlog en una lista de deseos.
- **Hay dos paletas y no son lo mismo.** El cromo del brief es la identidad de quien firma;
  la paleta por sector de `app_demo_guide.md` es la marca *del cliente* en la demo-app. No
  unificarlas: ver la nota en `references/palette.md`.
- **La escala de colores de áreas y prioridades codifica información, no marca.** Cada una
  va siempre acompañada de etiqueta de texto: el brief tiene que leerse igual en blanco y
  negro.

## DO

- Mantener `SKILL.md` y `README.md` de acuerdo en lo que la skill hace y no hace
- Probar un lead completo de principio a fin antes de publicar
- Mantener la versión en el frontmatter de `SKILL.md`
- Conservar la atribución al autor original (ver LICENSE)

## DON'T

- No publicar sin probar al menos un lead completo
- No prometer en el README nada que la skill no haga: usa búsqueda web, no APIs de
  registros oficiales, y así hay que contarlo
- No meter datos de clientes reales en ejemplos, nombres de fichero ni referencias
- No usar comercialmente sin permiso del autor
