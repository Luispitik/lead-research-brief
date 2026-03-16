# Lead Research Brief — Skill para Claude Code

Skill de **NorteIA** para investigar en profundidad un lead comercial, construir el mapa de procesos operativos AS-IS y generar una propuesta de app a medida.

## Que hace esta skill?

Dado un lead (organizacion + contexto), ejecuta una investigacion exhaustiva y genera **tres entregables sincronizados**:

1. **Resumen en chat** — hallazgos clave, fricciones detectadas y oportunidades IA
2. **HTML interactivo** — dos pestanas: Mapa de Procesos AS-IS + Funcionalidades app a medida
3. **Documento Word (.docx)** — informe estructurado listo para entregar

## Como funciona?

### Fase 0 — Formulario del lead
Recoge datos del lead: organizacion, sector, URL, contacto, problema, contexto y objetivo.

### Fase 1 — Investigacion exhaustiva
Usa busqueda web con 6-8 vectores por sector: la organizacion en si, software actual, normativa, benchmark de competencia, casos de uso IA, y dolores comunes.

### Fase 2 — Mapa de Procesos AS-IS
Construye entre 6 y 10 areas operativas con 6-9 pasos cada una, incluyendo actores, tipos de paso, integraciones y fricciones concretas.

### Fase 3 — Backlog de Funcionalidades
Disena entre 6 y 10 modulos de app a medida con funcionalidades priorizadas (Esencial / Recomendado / A valorar).

### Fase 4 — Generacion de entregables
Produce los tres artefactos: resumen en chat, HTML interactivo premium y documento Word.

## Sectores soportados

- Colegios profesionales y asociaciones
- PYMEs / Manufactura / Industria
- Despachos juridicos
- Clinicas y centros medicos
- Sector inmobiliario
- Sector educativo / Formacion
- Sector publico / Ayuntamientos
- Sector agricola / Agroalimentario

## Estructura del repositorio

```
SKILL.md                          # Skill principal
references/
  research_vectors.md             # Queries de investigacion por sector
  palette.md                      # Paleta de colores para areas y modulos
  pain_library.md                 # Biblioteca de fricciones por sector
  html_template_guide.md          # Guia de generacion del HTML premium
```

## Como instalar

En Claude Code, ejecuta:

```
/install-skill https://github.com/SalgadoIA/lead-research-brief
```

O copia la carpeta completa a `~/.claude/skills/lead-research-brief/`.

## Como usar

Di cualquiera de estas frases:
- "Investiga este lead: [nombre organizacion]"
- "Haz el brief de [organizacion]"
- "Genera el mapa de procesos de [organizacion]"
- "Prepara la propuesta para [organizacion]"

## Autor

**Luis Miguel Salgado Alonso** — [SalgadoIA](https://github.com/SalgadoIA)

Skill desarrollada como parte del framework NorteIA para automatizacion de propuestas comerciales B2B.


---

## Autor

Creado por **Luis Salgado** — **NorteIA** / **SalgadoIA**
- Web: [salgadoia.com](https://salgadoia.com)
- LinkedIn: [linkedin.com/in/luis-salgado-salgado](https://linkedin.com/in/luis-salgado-salgado)

---

> **¿Quieres skills como esta, personalizadas para tu negocio?**
>
> Esta es la versión genérica y open-source. En **NorteIA** diseñamos skills a medida para empresas: onboarding de clientes, generación de propuestas, automatización de procesos comerciales, y mucho más.
>
> Contacta con nosotros en [norteia.es](https://norteia.es) o [salgadoia.com](https://salgadoia.com)
