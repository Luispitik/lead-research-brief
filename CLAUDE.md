# CLAUDE.md — Lead Research Brief (Published Skill)

Repositorio Git publicado de la skill Lead Research Brief v1.0.0. Es el repo que se clona/instala. SKILL.md es el archivo principal que Claude lee.

## Estructura

```
SKILL.md              -- Skill principal (Claude lee este archivo)
README.md             -- Documentacion para GitHub (uso, instalacion)
LICENSE               -- CC BY-NC-SA 4.0
references/           -- Archivos de referencia (paleta, fricciones, queries, HTML)
  html_template_guide.md
  pain_library.md
  palette.md
  research_vectors.md
.git/                 -- Repo: github.com/Luispitik/lead-research-brief
```

## Key files

- `SKILL.md` — Skill principal que Claude ejecuta. No tocar sin leer completo
- `README.md` — Cara publica del repo. Incluye instrucciones de instalacion
- `references/` — Datos de soporte que la skill lee por fases

## DO

- Mantener SKILL.md y README.md sincronizados en mensajes
- Testear la skill completa antes de hacer push
- Incluir version semver en frontmatter de SKILL.md
- Citar autor (NorteIA/SalgadoIA) en cualquier modificacion (licencia CC BY-NC-SA)

## DON'T

- No hacer push sin testear al menos 1 lead completo
- No eliminar la atribucion del autor en SKILL.md
- No usar comercialmente sin permiso del autor
