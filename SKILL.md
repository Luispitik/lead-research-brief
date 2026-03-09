---
name: lead-research-brief
description: >
  Skill de NorteIA para investigar en profundidad un lead comercial, construir el mapa
  de procesos operativos AS-IS de su organización, generar el backlog de funcionalidades
  para una app a medida, y entregar tres artefactos: resumen en chat, HTML interactivo
  (estilo premium con dos pestañas: Mapa de Procesos + Funcionalidades) y documento Word.
  USAR SIEMPRE cuando el usuario diga "investiga este lead", "haz el brief de", "prepara
  la propuesta para", "quiero investigar a", "genera el mapa de procesos de", "necesito
  el brief de investigación de", "brief_investigacion", o proporcione un formulario de
  lead con nombre de organización, sector o problema. Aplica a cualquier tipo de
  organización: colegios, PYMEs, despachos, clínicas, ayuntamientos, asociaciones, etc.
---

# Brief · Investigación · Propuesta — Skill de NorteIA

## ¿Qué hace esta skill?

Dado un lead (organización + contexto), esta skill ejecuta una investigación exhaustiva
y genera tres entregables sincronizados:

1. **Resumen en chat** — hallazgos clave, fricciones detectadas y oportunidades IA
2. **HTML interactivo** — dos pestañas: Mapa de Procesos AS-IS + Funcionalidades app a medida
3. **Documento Word (.docx)** — informe estructurado listo para entregar o archivar

---

## FASE 0 — Recoger el formulario del lead

Si el usuario no ha proporcionado aún todos los datos, pedirle que rellene (o confirmar
los que ya dio):

```
FORMULARIO DE LEAD — BRIEF INVESTIGACIÓN PROPUESTA

1. Nombre de la organización:
2. Sector / actividad principal:
3. URL web (si existe):
4. Nombre del interlocutor/a y cargo:
5. Problema o necesidad detectada (en sus propias palabras):
6. Contexto adicional (tamaño, número de empleados, software actual conocido, etc.):
7. Objetivo de la reunión o de la propuesta:
```

Extraer del formulario: `org_name`, `sector`, `url`, `contact_name`, `contact_role`,
`pain_statement`, `context`, `goal`.

---

## FASE 1 — Investigación exhaustiva (web_search o launch_extended_search_task)

**OBLIGATORIO usar búsqueda web.** No inventar datos. Si hay herramienta de investigación
extendida disponible, usarla. Si solo hay web_search, hacer al menos 6-8 búsquedas
combinando los vectores siguientes:

### Vectores de investigación

Leer `references/research_vectors.md` para la guía completa de búsquedas por sector.

En resumen, investigar siempre:

| # | Vector | Ejemplo de query |
|---|--------|-----------------|
| 1 | Organización en sí | `"[org_name]" [ciudad] [sector]` |
| 2 | Software / herramientas actuales | `"[org_name]" software gestión OR ERP OR CRM` |
| 3 | Normativa sectorial relevante | `normativa [sector] España 2024 2025` |
| 4 | Benchmark competencia / equivalentes | `colegios [sector] España digitalización software` |
| 5 | Casos de uso IA en el sector | `inteligencia artificial [sector] automatización España` |
| 6 | Dolores comunes del sector | `[sector] problemas gestión ineficiencias digitalización` |
| 7 | Contexto regulatorio IA | `EU AI Act [sector] obligaciones riesgo` |
| 8 | Noticias recientes de la org | `"[org_name]" site:es OR noticias 2024 2025` |

### Qué extraer

- **Datos verificados de la organización**: tamaño, sede, web, redes, responsables
- **Software o herramientas actuales** (si se pueden inferir o encontrar)
- **Contexto normativo** que afecta al sector (fechas clave, obligaciones)
- **Fricciones comunes** del sector (validadas por el pain_statement del formulario)
- **Oportunidades IA** concretas y aplicables (no genéricas)
- **Integraciones externas** habituales del sector

---

## FASE 2 — Construir el Mapa de Procesos AS-IS

Con los datos investigados, identificar entre **6 y 10 áreas operativas** de la organización.

Para cada área construir:

```
Área {N}:
  id: snake_case_único
  label: "Nombre del área"
  icon: emoji representativo
  color: color HEX (asignar uno de la paleta: ver references/palette.md)
  light: versión clara del color (para fondos)
  desc: "Descripción de una línea de qué gestiona esta área"
  steps: [ entre 6 y 9 pasos, cada uno con:
    label: descripción del paso (acción concreta)
    actor: quién lo ejecuta (persona, sistema, organización externa)
    type: "entrada" | "proceso" | "decisión" | "integración" | "salida"
  ]
  integrations: [ 2-4 sistemas o plataformas externas relevantes ]
  pains: [ 2-4 fricciones actuales concretas y verificadas ]
```

**Reglas de calidad del mapa:**
- Cubrir el ciclo de vida completo de la organización (no solo lo que mencionó el lead)
- Al menos un paso de tipo `integración` por área
- Los `pains` deben ser concretos y ligados al sector (no genéricos)
- Los actores deben ser realistas para el tamaño de la organización

---

## FASE 3 — Construir el Backlog de Funcionalidades

Diseñar entre **6 y 10 módulos** de una app a medida que resuelva los pain points del mapa.

Para cada módulo:

```
Módulo {N}:
  cat: "Nombre del módulo"
  icon: emoji
  color: color HEX de la paleta
  items: [ entre 3 y 6 funcionalidades, cada una con:
    label: "Nombre de la funcionalidad"
    desc: "Descripción de qué hace y qué problema resuelve (2-3 líneas)"
    prioridad: "Esencial" | "Recomendado" | "A valorar"
  ]
```

**Reglas de priorización:**
- `Esencial`: resuelve el pain principal del lead, obligatorio en MVP
- `Recomendado`: alto valor, implementar en segunda fase
- `A valorar`: interesante pero no crítico, para valorar con el cliente

Cada módulo debe corresponder a al menos un área del mapa de procesos.
Incluir siempre un módulo de **IA Aplicada** y uno de **Cumplimiento / Gobernanza**.

---

## FASE 4 — Generar los tres entregables

### 4A — Resumen en chat

Responder en el chat con esta estructura:

```
## Brief: [Nombre organización]

**Interlocutor/a:** [nombre] · [cargo]
**Sector:** [sector] · **Tamaño estimado:** [dato]

### Hallazgos clave
- [hallazgo 1 con dato concreto]
- [hallazgo 2]
- ...

### Fricciones principales detectadas
- [fricción 1 — área]
- [fricción 2 — área]
- ...

### Oportunidades IA prioritarias
1. [oportunidad con impacto esperado]
2. ...

### Ecosistema digital actual
[software/herramientas detectadas]

### Contexto normativo relevante
[normativa + fechas clave que crean urgencia]
```

### 4B — HTML interactivo

Leer `references/html_template_guide.md` para la guía completa de generación del HTML.

En resumen:
- Estructura idéntica a `procesos_premium.html` (misma estética, mismos colores CSS)
- Dos pestañas en nav: **Mapa de Procesos** / **Funcionalidades**
- Los datos de AREAS[] y FUNCIONALIDADES[] se inyectan con los datos del lead
- El nombre de la organización aparece en el nav y en los títulos de sección
- Guardar como `brief_[org_slug]_[YYYYMMDD].html` en /mnt/user-data/outputs/

### 4C — Documento Word (.docx)

Leer `/mnt/skills/public/docx/SKILL.md` para generar el Word correctamente.

Estructura del Word:
1. Portada (nombre org, fecha, ref, NorteIA)
2. Resumen ejecutivo (hallazgos, fricciones, oportunidades)
3. Mapa de Procesos AS-IS (tabla por área: pasos + integraciones + fricciones)
4. Propuesta de Funcionalidades (tabla por módulo con prioridad)
5. Contexto normativo y oportunidad IA
6. Próximos pasos recomendados

Guardar como `brief_[org_slug]_[YYYYMMDD].docx` en /mnt/user-data/outputs/

---

## FASE 5 — Presentar al usuario

Usar `present_files` con ambos archivos (HTML primero, luego Word).
Confirmar en el chat que la investigación está completa y ofrecer ajustes.

---

## Referencias de esta skill

- `references/research_vectors.md` — guía de búsquedas por sector con queries tipo
- `references/html_template_guide.md` — guía completa del HTML premium + datos de colores
- `references/palette.md` — paleta de colores por área/módulo
- `references/pain_library.md` — biblioteca de fricciones comunes por sector

Leer solo la referencia necesaria en cada fase. No cargarlas todas a la vez.
