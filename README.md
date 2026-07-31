# Lead Research Brief

**Skill de Claude que convierte un lead B2B en un diagnóstico operativo defendible.**
Le das el nombre de una organización y el problema que te ha contado; te devuelve el mapa
de cómo trabaja hoy, dónde se le atasca el trabajo y qué software resolvería cada atasco
— en tres formatos que puedes llevar a una reunión.

Pensada para consultores, agencias y desarrolladores a medida que necesitan llegar a la
primera reunión sabiendo más del negocio del cliente que lo que el cliente contó en el
formulario.

---

## El problema que resuelve

La primera reunión con un lead B2B se suele preparar de dos maneras: mirando su web diez
minutos, o no preparándola. Las dos acaban igual — una reunión en la que el consultor
pregunta y el cliente explica, cuando debería ser al revés.

Esta skill invierte esa reunión. Llegas con un mapa de los procesos de su sector ya
dibujado, con las fricciones típicas ya nombradas y con la normativa que le aprieta ya
fechada. El cliente corrige detalles en vez de explicar desde cero, y esa corrección **es**
el descubrimiento.

---

## Qué hace, paso a paso

| Fase | Qué ocurre | Salida |
|---|---|---|
| 0 | Recoge un formulario de 7 campos sobre el lead | — |
| 1 | Investigación web: 8 vectores de búsqueda adaptados al sector | Datos verificados |
| 2 | Construye el **mapa de procesos AS-IS**: 6-10 áreas operativas, cada una con 6-9 pasos, actores, integraciones externas y fricciones | Estructura de datos |
| 3 | Diseña el **backlog**: 6-10 módulos de app a medida, cada funcionalidad priorizada Esencial / Recomendado / A valorar | Estructura de datos |
| 4 | Genera los tres entregables | Chat + HTML + DOCX |
| 5 | Los presenta y ofrece ajustes | — |
| 6 | *(Opcional, bajo petición)* Demo-app funcional con datos sintéticos y branding del cliente | HTML |

Las fases 2 y 3 están acopladas a propósito: **cada módulo del backlog tiene que resolver
al menos una fricción del mapa.** Es lo que impide que el backlog se convierta en una lista
de funcionalidades bonitas sin justificación operativa.

---

## Con qué fuentes trabaja

**Importante: esta skill usa búsqueda web, no APIs de registros oficiales.** No consulta
bases de datos por identificador ni descarga ficheros de fuentes públicas. Lo que aporta es
**hacia dónde apuntar la búsqueda**: para cada sector trae las queries, los sistemas que ese
sector suele tener instalados y la normativa que le afecta con sus fechas.

Fuentes que la skill instruye a priorizar en las búsquedas:

- Dominios `.es`, BOE y diarios oficiales autonómicos
- BORME, Axesor o Infoempresa para datos societarios básicos
- LinkedIn para identificar interlocutores y cargos
- Webs y prensa sectorial

Y, según el sector del lead, dirige la investigación hacia el ecosistema que le corresponde
— LexNET y CGPE en el jurídico; FUNDAE y SEPE en formación; FEGA y SIGPAC en agro; Cl@ve y
Registro Electrónico en administración local; AEAT y Verifactu en casi todos.

Si lo que buscas es descubrimiento masivo de empresas consultando registros oficiales de
forma programática, esta skill no es eso. Esto trabaja **un** lead concreto en profundidad.

### Sectores con vectores y biblioteca de fricciones propios

Colegios profesionales y asociaciones · PYME industrial y manufactura · Despachos jurídicos
· Clínicas y centros médicos · Inmobiliario · Formación y centros educativos · Ayuntamientos
y sector público · Agro y cooperativas · Staffing y workforce management.

Para un sector no listado, la skill usa las reglas transversales y lo documenta como tal.

---

## Qué NO hace

Conviene decirlo antes de que alguien lo descubra a mitad de una demo:

- **No consulta APIs de registros oficiales.** Investiga con búsqueda web dirigida.
- **No verifica lo que encuentra contra una fuente primaria.** Distingue en el informe
  entre dato verificado y dato inferido del sector, pero la verificación última es tuya.
- **No calcula precios, plazos ni presupuestos.** El backlog está priorizado, no valorado.
- **No es un CRM ni escribe en uno.** Genera ficheros; dónde los guardas es cosa tuya.
- **No implementa nada.** El backlog describe la app; construirla es otro trabajo.
- **No inventa datos para rellenar huecos.** Si no encuentra la organización, lo dice y
  trabaja con benchmark sectorial declarado como tal.
- **La demo-app de la Fase 6 es una maqueta con datos sintéticos.** No se conecta a nada,
  no tiene backend, y lleva un aviso visible de que sus respuestas de IA están
  pre-configuradas. Enseñarla como producto terminado sería mentir.

---

## Instalación

### Claude Code

```bash
git clone https://github.com/Luispitik/lead-research-brief.git ~/.claude/skills/lead-research-brief
```

### Claude.ai

Ajustes → Capacidades → Skills → crear skill nueva. Pega `SKILL.md` como contenido
principal y sube `references/` conservando la estructura de carpetas.

### Dependencia recomendada

La Fase 4C genera un `.docx` apoyándose en la skill `docx`, disponible de serie en
claude.ai. Sin ella obtendrás el resumen en chat y el HTML, pero no el Word.

### Nota de portabilidad

`SKILL.md` está escrito para claude.ai: guarda los entregables en el directorio de salidas
de ese entorno y busca la skill `docx` en su ruta estándar. En Claude Code funciona igual
salvo por eso — dile dónde quieres los ficheros, o cambia las dos rutas en `SKILL.md` por
las tuyas.

---

## Uso

```
Investiga este lead: [organización], sector [X], me han dicho que [problema]
```

También responde a "haz el brief de…", "prepara la propuesta para…" o "genera el mapa de
procesos de…". Si faltan datos, pide el formulario de 7 campos antes de empezar.

La Fase 6 **no se ejecuta sola**. Hay que pedirla:

```
Genera la demo-app para la reunión
```

---

## Ejemplo de salida

Con un lead ficticio — una cooperativa agrícola de 40 socios que dice "perdemos horas
cuadrando el cuaderno de campo" — el resumen en chat sale así:

```
## Brief: Cooperativa Agrícola [Nombre]

Interlocutor: [nombre] · Gerente
Sector: Agroalimentario · Tamaño estimado: 40 socios, 1 almacén

### Hallazgos clave
- El cuaderno de explotación digital es obligatorio desde 2024; siguen en papel
- Sin ERP: la gestión de almacén vive en una hoja de cálculo compartida
- Cobros de la PAC gestionados socio a socio, sin visibilidad agregada

### Fricciones principales detectadas
- Trazabilidad de lote rota entre campo y almacén (área: Recepción)
- Cuaderno de campo en papel, con riesgo de sanción (área: Cumplimiento)
- Sin previsión de cobros PAC (área: Financiero)

### Oportunidades IA prioritarias
1. Extracción automática de albaranes a registro de entrada
2. Alerta de plazos normativos por explotación

### Contexto normativo relevante
Cuaderno digital obligatorio · Verifactu para facturación electrónica
```

Y el mapa de procesos se construye con esta forma por área:

```
Área: recepcion_producto
  desc: "Entrada de producto desde las explotaciones al almacén"
  steps:
    - "El socio avisa de la descarga"       actor: Socio           type: entrada
    - "Pesaje en báscula"                   actor: Almacén         type: proceso
    - "¿Cumple parámetros de calidad?"      actor: Técnico         type: decisión
    - "Registro de lote en cuaderno"        actor: Almacén         type: proceso
    - "Volcado a SIGPAC"                    actor: Sistema         type: integración
    - "Albarán al socio"                    actor: Administración  type: salida
  integrations: [SIGPAC, FEGA, laboratorio externo]
  pains: ["El lote se anota a mano y se pierde el vínculo con la explotación",
          "El albarán se emite en papel y se archiva sin digitalizar"]
```

El HTML lo renderiza como tarjetas navegables con vista de detalle por área; el DOCX, como
tablas. Los tres entregables salen de los mismos datos, así que no pueden contradecirse.

---

## Arquitectura

```
SKILL.md                        Orquestador: 6 fases, la 6ª opcional
references/
  research_vectors.md           Queries de búsqueda por sector
  pain_library.md               Fricciones típicas por sector
  html_template_guide.md        Especificación del HTML interactivo
  palette.md                    Colores y escalas categóricas
  app_demo_guide.md             Guía de la demo-app (Fase 6)
```

Las referencias se leen **por fase**, no todas de golpe. Es lo que mantiene el contexto
manejable en un brief largo.

### Personalizar el cromo

El HTML sale con una paleta neutra editorial. Para ponerle tu marca, cambia los valores en
`references/palette.md` y `references/html_template_guide.md` — están duplicados a propósito
para que la plantilla siga siendo legible por sí sola.

Lo que **no** conviene tocar: la escala de 8 colores de las áreas y la de prioridades. Esas
codifican información dentro del diagrama, no identidad. Y cada una lleva siempre etiqueta
de texto, para que el brief se lea igual fotocopiado en blanco y negro.

---

## Licencia

**CC BY-NC-SA 4.0** — uso, modificación y redistribución libres para fines **no
comerciales**, citando al autor y manteniendo la misma licencia.

Para uso comercial hace falta permiso expreso. Ver [LICENSE](./LICENSE).

---

Creado por **Luis Salgado** — [salgadoia.com](https://salgadoia.com)
