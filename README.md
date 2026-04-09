# Lead Research Brief v1 — Claude Skill

> Skill para Claude que investiga en profundidad un lead comercial, construye el mapa de procesos operativos AS-IS de su organizacion, genera el backlog de funcionalidades para una app a medida, y entrega tres artefactos profesionales.

**Creado por [NorteIA](https://norteia.es) / [SalgadoIA](https://salgadoia.com)**

---

## Que hace

Lead Research Brief es una skill para Claude que convierte un formulario de lead en un analisis operativo completo. Dados los datos basicos de una organizacion (nombre, sector, problema), ejecuta:

1. **Investigacion exhaustiva** — 8 vectores de busqueda web por sector (organizacion, software, normativa, competencia, IA, dolores, regulacion, noticias)
2. **Mapa de procesos AS-IS** — 6-10 areas operativas con pasos, actores, integraciones y fricciones concretas
3. **Backlog de funcionalidades** — 6-10 modulos priorizados (Esencial / Recomendado / A valorar) con IA aplicada y cumplimiento incluidos
4. **3 entregables sincronizados**:
   - Resumen estructurado en chat
   - HTML interactivo premium (dos pestanas: Mapa de Procesos + Funcionalidades)
   - Documento Word (.docx) listo para entregar

## Sectores cubiertos

La skill incluye vectores de investigacion y biblioteca de fricciones para:

- Colegios profesionales y asociaciones
- PYMEs / Industria / Manufactura
- Despachos juridicos
- Clinicas y centros medicos
- Sector inmobiliario
- Sector educativo / Formacion
- Sector publico / Ayuntamientos
- Sector agricola / Agroalimentario
- Fricciones transversales (facturacion electronica, RGPD, EU AI Act, firma digital)

## Arquitectura

```
SKILL.md                              -> Skill principal (5 fases)
references/
  research_vectors.md                 -> Queries de busqueda por sector
  pain_library.md                     -> Biblioteca de fricciones por sector
  html_template_guide.md              -> Guia del HTML interactivo premium
  palette.md                          -> Paleta de colores y tipos de paso
```

## Instalacion

### En Claude.ai (Web)

1. Ve a **Personalizar** -> **Skills**
2. Crea una nueva skill
3. Copia el contenido de `SKILL.md` como skill principal
4. Sube los archivos de `references/` manteniendo la estructura de carpetas

### En Claude Code (CLI)

```bash
# Clona el repositorio en tu directorio de skills
git clone https://github.com/Luispitik/lead-research-brief.git ~/.claude/skills/lead-research-brief
```

## Uso

Simplemente di a Claude cualquiera de estas frases:

- "Investiga este lead"
- "Haz el brief de [organizacion]"
- "Prepara la propuesta para [empresa]"
- "Genera el mapa de procesos de [organizacion]"
- "Brief de investigacion de [empresa]"

La skill te pedira un formulario con 7 campos y ejecutara las 5 fases automaticamente.

## Skills complementarias recomendadas

| Skill | Para que |
|-------|----------|
| `docx` | Generar el documento Word correctamente |
| `business-launcher` | Lanzar un negocio completo desde cero |

## Entregables que genera

| # | Entregable | Formato |
|---|-----------|---------|
| 1 | Resumen ejecutivo | Chat (markdown) |
| 2 | Diagnostico operativo interactivo | HTML (autocontenido) |
| 3 | Informe de investigacion | DOCX |

---

## Licencia

**CC BY-NC-SA 4.0** — Puedes usar, modificar y redistribuir esta skill libremente para uso **no comercial**, siempre que:

1. **Cites al autor original**: NorteIA / SalgadoIA — Luis Salgado
2. **Incluyas un enlace** a este repositorio
3. **Distribuyas modificaciones** bajo la misma licencia
4. **No la uses comercialmente** sin permiso expreso del autor

Para uso comercial, contacta con: contacto@norteia.es

Ver [LICENSE](./LICENSE) para el texto completo.

---

## Creditos

Creado por **Luis Salgado** — [NorteIA](https://norteia.es) / [SalgadoIA](https://salgadoia.com)

- Web: [salgadoia.com](https://salgadoia.com)
- LinkedIn: [linkedin.com/in/luis-salgado-salgadoia](https://linkedin.com/in/luis-salgado-salgadoia)

---

> **Quieres skills como esta, personalizadas para tu negocio?**
>
> Esta es la version open-source de Lead Research Brief. En [NorteIA](https://norteia.es) disenamos skills a medida para consultoras, despachos y empresas de servicios: investigacion de leads, generacion de propuestas, automatizacion de procesos comerciales, y mucho mas.
>
> **Contacta con nosotros en [norteia.es](https://norteia.es) o [salgadoia.com](https://salgadoia.com)**
