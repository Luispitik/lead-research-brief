# Guía de la Demo-App Pre-Reunión (Fase 6)

## Objetivo

Generar un **único archivo HTML autocontenido** que sea una mini-aplicación funcional,
con datos sintéticos del sector del lead y branding del cliente, para que el operador
la enseñe en vivo en la reunión comercial como si fuera un producto ya existente.

---

## Stack técnico (obligatorio)

CDNs únicamente — sin npm, sin build, sin servidor.

```html
<!-- Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Space+Grotesk:wght@500;600;700&display=swap" rel="stylesheet">

<!-- Runtime -->
<script crossorigin src="https://unpkg.com/react@18.3.1/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@18.3.1/umd/react-dom.production.min.js"></script>
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/@babel/standalone@7.24.0/babel.min.js"></script>
```

Render con `ReactDOM.createRoot(document.getElementById('root')).render(<App />);` dentro
de un `<script type="text/babel" data-presets="react">...</script>`.

Icons: SVG inline (lucide-like). No depender de librerías externas de iconos.
Charts: SVG inline (sparklines, barras simples). No recharts — evita fallos de CDN.

---

## Layout base (obligatorio)

```
<div class="flex h-screen overflow-hidden">
  <Sidebar />                         <!-- 256px fijo, color primario del cliente -->
  <div class="flex-1 flex flex-col overflow-hidden">
    <Topbar />                        <!-- 72px -->
    <main class="flex-1 overflow-y-auto">
      <div class="max-w-[1400px] mx-auto p-8 fade-in" key={view}>
        <ViewX />
      </div>
    </main>
  </div>
</div>
```

### Sidebar obligatorio

- Header: logo (con fallback monograma de 2 letras sobre fondo accent) + nombre cliente + tagline
- Nav: Home + 2-3 items módulo + AI Assistant (siempre el último)
- Footer: user card con iniciales + rol

### Topbar obligatorio

- Izquierda: breadcrumb dinámico (uppercase small + título + subtítulo del sector)
- Derecha: botón **Reset demo** (restaura seeds + borra localStorage) + bell con badge

---

## Vistas (4 fijas)

1. **Home / Dashboard**: hero con saludo al usuario, 4 KPIs, 2-3 cards de módulos que enlazan, bloque de actividad reciente + bloque lateral con próximos/alertas.
2. **Módulo 1**: el que resuelve el pain principal del lead. Suele ser una bandeja o queue con detalle lateral + CRUD.
3. **Módulo 2** (o **Módulo 2+3** si cabe): dashboard con drill-down, tablas, acciones.
4. **Asistente IA**: 2 columnas. Izquierda = 4 preset actions, derecha = chat con user bubbles (primary) + assistant bubbles (slate-100), input libre con respuesta genérica.

---

## Datos sintéticos — patrones por sector

### Regla general

- **Entidad principal**: 20-40 registros.
- **Entidades secundarias**: 8-15 registros.
- Nombres realistas del país del cliente. Para ES/LATAM mezclar castellanos + locales. Para US mezclar inglés + latino + afroamericano.
- Direcciones y lugares del país del cliente.
- Fechas recientes (últimos 7-30 días) usando helpers `hoursAgo(h)` / `hoursAhead(h)`.

### Plantilla de helpers (reutilizable)

```js
const hoursAgo = (h) => new Date(Date.now() - h * 3600 * 1000).toISOString();
const hoursAhead = (h) => new Date(Date.now() + h * 3600 * 1000).toISOString();
const timeAgo = (iso) => { /* "42m ago", "3h ago", "2d ago" */ };
const timeIn  = (iso) => { /* "in 2h", "in 3d", "overdue" */ };
```

### Sectores

**Colegio / Escuela**: entidad principal = mensajes familia-centro (con categorías académico/salud/administrativo/evento/queja). Entidades: alumnos, cursos, eventos, alertas.

**Staffing / RR.HH.**: entidad principal = orders abiertas (cliente + rol + seats + pay + urgencia). Entidades: workers (skills, disponibilidad, compliance I-9/drug/physical), compliance alerts.

**Clínica / Centro médico**: entidad principal = citas (paciente + médico + hora + estado). Entidades: pacientes, profesionales, alertas de resultados, lista de espera.

**Despacho jurídico**: entidad principal = expedientes (matter number + cliente + tipo + responsable + plazos). Entidades: notificaciones LexNET, eventos de agenda, facturación pendiente.

**PYME industrial**: entidad principal = órdenes de producción (lote + producto + cliente + plazo). Entidades: stock, proveedores, incidencias.

**Agrícola / Cooperativa**: entidad principal = campañas (lote + cultivo + estado + parcelas). Entidades: socios, tratamientos, cuaderno de campo.

**Ayuntamiento**: entidad principal = expedientes ciudadanos (trámite + solicitante + estado + plazo). Entidades: registros, quejas, eventos.

**Inmobiliaria**: entidad principal = leads (portal + interés + seguimiento). Entidades: inmuebles, visitas, cierres.

---

## Librería de IA mock — patrones por categoría

Cada demo-app tiene **4 presets** en el Asistente IA, siempre cableados con respuestas
pre-baked. Redactar las respuestas *al generar la demo* usando el dataset sintético
y el sector del cliente.

### Categorías canónicas (elegir 4, una por columna)

| Categoría      | Qué hace                                    | Ejemplo trigger                                         |
|----------------|---------------------------------------------|---------------------------------------------------------|
| **Resumen**    | Condensa lo urgente en 5-7 bullets          | "Resume los mensajes/órdenes sin responder más urgentes"|
| **Redacción**  | Escribe un artefacto final (email, circular, anuncio) | "Redacta una circular para familias / un job ad en ES" |
| **Análisis**   | Detecta patrones con tabla + recomendación  | "Detecta patrones de turnover / quejas / incidentes"    |
| **Informe**    | Produce un reporte estructurado con tabla   | "Informe semanal de incidencias por curso / cliente"    |

### Formato de cada respuesta pre-baked

- Markdown con **bold**, listas, tablas cuando aplique.
- Citar datos concretos del dataset sintético (nombres, IDs, fechas).
- Terminar con **Recomendación** o **Próximos pasos** accionables.
- Longitud: 150-400 palabras. Ni demasiado corto (no impresiona) ni largo (no lee en reunión).

### Ejemplo de respuesta baked — staffing, categoría Análisis

```
**90-day turnover analysis — top 5 clients**

| Client              | Deployed | Left <30d | 90-day retention | vs avg |
|---------------------|---------:|----------:|-----------------:|-------:|
| Logística ATL6      | 84       | 22        | **52%**          | −8 pts |
| ...                                                                     |

**Pattern detected**
Logística ATL6 is 8 points below average. Early departures cluster in week 2,
transportation gaps after first paycheck. 14 of 22 leavers cited shift-swap
inflexibility.

**Recommended actions**
1. Pilot same-day pay → +6 pts retention.
2. Bilingual shift-swap board → +3 pts.
3. Week 1-2-3 check-in cadence → +4 pts.

*Annualized revenue impact: ~$340K avoided rehire cost.*
```

---

## Branding del cliente

### Extracción del logo

1. Inspeccionar la web del cliente en busca del logo.
2. Rutas habituales:
   - `/logo.png`, `/logo.svg`
   - `/brand/<slug>.png`, `/brand/<slug>-icon.png`
   - `/assets/logo.*`, `/static/logo.*`
   - `/_next/image?url=%2Fbrand%2F...` (sitios Next.js)
   - `<meta property="og:image" content="...">`
   - `/favicon.ico` como último recurso
3. Usar la URL absoluta en el `<img src>`:
   ```jsx
   function Logo({ className }) {
     const [failed, setFailed] = useState(false);
     if (failed) {
       return <div className={cn('rounded-lg bg-accent flex items-center justify-center text-white font-bold', className)}>
         <span className="text-[13px]">{ORG.short.slice(0, 2)}</span>
       </div>;
     }
     return <div className={cn('rounded-lg bg-white flex items-center justify-center p-1', className)}>
       <img src={ORG.logo_src} alt={ORG.short} onError={() => setFailed(true)}
            className="max-w-full max-h-full object-contain" />
     </div>;
   }
   ```

### Extracción de paleta

- Inspeccionar CSS/HTML del cliente: variables CSS (`--brand: #...`), clases Tailwind
  (bg-blue-900), atributos inline.
- Si no hay, usar `<meta name="theme-color">`.
- Fallback: paleta neutral por sector:

> **NO SUSTITUYAS ESTA TABLA POR EL CROMO DEL BRIEF.** Estos colores son la marca **del
> cliente**, no la tuya: la demo-app existe para que el cliente se vea a sí mismo, y
> pintarla con tu paleta haría que todas las demos parecieran tuyas, que es justo lo
> contrario de lo que busca esa pieza. El cromo del brief se aplica al **brief** (ver
> `references/palette.md` y `references/html_template_guide.md`), nunca a la demo.

| Sector                       | Primario        | Accent              | Notas                       |
|------------------------------|-----------------|---------------------|-----------------------------|
| Colegio / Educación          | Navy `#1E3A5F`  | Gold `#C9A869`      | Serio, institucional        |
| Clínica / Sanidad            | Teal `#0E7C7B`  | Coral soft `#F28482`| Calmo, confiable            |
| Staffing / Warehouse / Ops   | Navy `#0B2545`  | Safety `#F97316`    | Industrial, urgencia        |
| Despacho jurídico            | Burgundy `#6B1E24` | Gold `#C9A84C`   | Formal, tradición           |
| PYME industrial              | Slate `#334155` | Orange `#EA580C`    | Técnico                     |
| Agro / Cooperativa           | Forest `#14532D`| Harvest `#EAB308`   | Natural                     |
| Ayuntamiento                 | Navy `#0A3D62`  | Red institucional `#B91C1C` | Institucional oficial |
| Inmobiliaria                 | Charcoal `#1F2937`| Gold `#B8860B`    | Sobrio                      |

### Tipografía

- **Display (títulos)**: Space Grotesk 500-700 para ops/staffing/industrial; Playfair Display 600-700 para educación/sanidad/jurídico.
- **Body (UI)**: Inter 400-700 en todos.

---

## CRUD mínimo (obligatorio)

El demo debe permitir al menos 2 de estas acciones:
- Marcar item como resuelto / respondido
- Despachar / asignar
- Crear nuevo item (modal con form)
- Descartar item
- Reset demo completo

Estado en React + persistencia en `localStorage` con key versionada:
```js
const STORAGE_KEY = '[org_slug]-demo-v1';
```

---

## Naming del archivo de salida

```
demo_[org_slug]_[YYYYMMDD].html

Ejemplos:
  demo_colegio_profesional_20260429.html
  demo_operador_logistico_20260422.html
  demo_clinica_dental_20260510.html
```

`org_slug` = nombre en minúsculas sin tildes, espacios → guión bajo, máx 4 palabras.

---

## Checklist de calidad antes de entregar

- [ ] Abre correctamente en Chrome/Firefox/Safari sin errores de consola
- [ ] Las 4 vistas cargan sin fallos
- [ ] El logo del cliente se muestra o cae limpiamente al monograma
- [ ] La paleta del cliente está aplicada en sidebar, botones primary y highlights
- [ ] Los datos sintéticos son realistas para el sector y el país del cliente
- [ ] Los 4 presets de IA devuelven respuestas pre-baked con datos concretos del dataset
- [ ] Al menos 2 acciones CRUD funcionan (click → cambio de estado visible)
- [ ] localStorage persiste el estado al recargar
- [ ] Reset demo restaura al estado inicial
- [ ] Footer del AI Assistant incluye nota de "Demo — respuestas pre-configuradas"
- [ ] El idioma del contenido coincide con el del cliente
- [ ] El tono del contenido coincide con el sector
- [ ] No hay placeholders visibles tipo "Lorem ipsum" o "TODO"
- [ ] El archivo es 100% offline tras la primera carga (CDNs cacheados)
