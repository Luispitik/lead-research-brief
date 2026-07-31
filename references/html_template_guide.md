# Guía de Generación del HTML Interactivo — Brief Investigación Propuesta

## Objetivo

Generar un archivo HTML autocontenido, sin dependencias externas salvo Google Fonts,
que sea visualmente idéntico al template `procesos_premium` de referencia.

---

## Estructura del archivo HTML

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <!-- Fonts: Playfair Display + DM Sans desde Google Fonts -->
  <!-- CSS completo embebido en <style> -->
</head>
<body>
  <nav>                        <!-- Nav sticky con pestañas -->
  <div id="tab-map" class="panel active">
    <div id="map-overview">   <!-- Grid de tarjetas de áreas -->
    <div id="map-detail">     <!-- Vista de detalle de área (oculta por defecto) -->
  </div>
  <div id="tab-func" class="panel">
    <div id="func-panel">     <!-- Acordeones de funcionalidades -->
  </div>
  <script>                     <!-- Datos + lógica embebidos -->
</body>
```

---

## CSS — Variables obligatorias

```css
:root {
  /* --- CROMO DEL BRIEF: identidad de quien firma el entregable -------------
     Default neutro y editorial. Si tienes marca propia, sustituye estos
     valores (y los de references/palette.md) por los tuyos.
     Regla 90·9·1: ~90% superficie neutra · ~9% tinta · ~1% acento. */
  --cream:       #F7F3EA;   /* fondo general, neutro cálido */
  --white:       #FFFFFF;
  --navy:        #0A1232;   /* tinta   — nav, titulares */
  --navy-light:  #6E6759;   /* piedra  — secundario */
  --text:        #0A1232;   /* tinta */
  --muted:       #6E6759;   /* piedra */
  --border:      #DCD4C2;   /* filete */
  --gold:        #2020FF;   /* ÚNICO acento. El nombre de la variable es
                               histórico: el valor ya no es dorado. */

  /* --- SEMÁNTICOS: siempre acompañados de etiqueta de texto -------------- */
  --red:         #B0453C;   /* Alerta */
  --red-light:   #ECE5D6;   /* Arena — fondo neutro, el color vive en el texto */
  --green:       #2F7A52;   /* Éxito */
  --green-light: #ECE5D6;   /* Arena */
  --amber:       #A97A1F;   /* Aviso */
  --amber-light: #ECE5D6;   /* Arena */

  /* --- ESCALA CATEGÓRICA del mapa de áreas: NO es marca -------------------
     Codifica áreas del negocio del cliente dentro del diagrama, no identidad.
     Se conserva a propósito (ver references/palette.md). Obligatorio:
     cada área lleva su ETIQUETA de texto; el color nunca va solo. */
  --blue:        #1B6CA8;
  --blue-mid:    #2E86C1;
  --blue-light:  #D6EAF8;
  --teal:        #0E7C7B;
  --teal-light:  #D1F2EB;
  --purple:      #6C3483;
  --purple-light:#F4ECF7;
}
```

---

## Nav — especificación

```html
<nav>
  <!-- Lado izquierdo: logo + separador + subtítulo -->
  <div class="nav-brand">
    <span class="nav-logo">[BRAND]</span>  <!-- marca del operador/consultora -->
    <div class="nav-divider"></div>
    <!-- Aquí va: "[Nombre org] · Diagnóstico Operativo" -->
    <span class="nav-subtitle">[ORG_NAME] · Diagnóstico Operativo</span>
  </div>
  <!-- Lado derecho: dos botones de pestaña -->
  <div class="nav-tabs">
    <button class="tab-btn active" data-tab="map">Mapa de Procesos</button>
    <button class="tab-btn" data-tab="func">Funcionalidades</button>
  </div>
</nav>
```

Estilos clave del nav:
- `background: var(--navy)` · `height: 64px` · `position: sticky; top: 0; z-index: 100`
- `.nav-logo`: Playfair Display 19px bold, color #fff
- `.tab-btn`: border redondeado, fondo transparente, color rgba(255,255,255,.55)
- `.tab-btn.active`: border blanco, fondo rgba(255,255,255,.15), color #fff

---

## Pestaña Mapa de Procesos — especificación

### Cabecera de sección

```html
<div class="section-title">Mapa de Procesos Operativos</div>
<div class="section-subtitle">
  Estado actual (AS-IS) · [N] áreas · [M] pasos identificados · [K] puntos de integración externa
</div>
<div class="gold-bar"></div>  <!-- width:56px height:3px background:var(--gold) -->
```

### Ecosystem chips bar

```html
<div class="ecosystem-bar">
  <span class="eco-label">Ecosistema digital</span>
  <!-- Un chip por sistema/integración detectada en la investigación -->
  <span class="eco-chip">[Sistema 1]</span>
  ...
</div>
```

### Grid de tarjetas (overview)

- `display: grid; grid-template-columns: repeat(auto-fill, minmax(340px, 1fr)); gap: 20px`
- Cada tarjeta: `background: white; border-radius: 14px; border-top: 4px solid [color_area]`
- Al hacer click abre la vista de detalle (ocultar overview, mostrar detail)
- Animación de entrada: `fadeInUp` con `animation-delay` escalonado por tarjeta

Contenido de cada tarjeta:
1. Icono + label + desc
2. 4 primeros pasos como chips coloreados por tipo (+ "N pasos más")
3. Sección "Áreas de mejora" con 2 primeras fricciones + "y N más →"

### Vista de detalle (al hacer click en tarjeta)

- Botón "← Volver al mapa general"
- Header: icono grande + título en color del área + desc
- Layout dos columnas:
  - **Columna principal** (flex:1): flujo de pasos numerados con línea vertical conectora
  - **Columna lateral** (340px): dos boxes apilados:
    - "Integraciones externas" (borde top color del área, chips teal)
    - "Fricciones identificadas" (borde top #E8A0A0, chips rojo claro)

Cada paso del flujo:
- Número circular coloreado según tipo
- Línea vertical conectora (excepto el último)
- Card con label, actor y badge de tipo

---

## Pestaña Funcionalidades — especificación

### Cabecera

```html
<div class="section-title">Funcionalidades de la aplicación</div>
<div class="section-subtitle">[N] funcionalidades en [M] módulos</div>
<div class="gold-bar"></div>
```

### Leyenda de prioridad

```html
<div class="priority-legend">
  <span class="legend-label">Prioridad</span>
  <div class="legend-item">
    <div class="legend-dot" style="background:#E74C3C"></div>
    <span class="legend-text">Esencial</span>
  </div>
  <div class="legend-item">
    <div class="legend-dot" style="background:#F39C12"></div>
    <span class="legend-text">Recomendado</span>
  </div>
  <div class="legend-item">
    <div class="legend-dot" style="background:#AEB6BF"></div>
    <span class="legend-text">A valorar</span>
  </div>
</div>
```

### Acordeones

- Un acordeón por módulo
- Header: icono + título (Playfair Display 16px) + contador "N funcionalidades · M esenciales"
- Toggle: `+` que rota a `×` al abrir
- Solo un acordeón abierto a la vez
- Al abrir: `border-top: 4px solid [color_modulo]`
- Cada ítem: label (DM Sans 14px bold) + desc (12px muted) + badge de prioridad (pill coloreado)

---

## JavaScript — estructura de datos

```javascript
// Objeto de tipos de paso (FIJO, no cambiar)
const TIPO = {
  "entrada":     { bg:"#EBF5FB", color:"#1A5276", border:"#AED6F1", label:"Entrada" },
  "proceso":     { bg:"#FDFEFE", color:"#2C3E50", border:"#D5D8DC", label:"Proceso" },
  "decisión":    { bg:"#FEFBE8", color:"#7D6608", border:"#F9E79F", label:"Decisión" },
  "integración": { bg:"#E8F8F5", color:"#1D6A39", border:"#A9DFBF", label:"Integración" },
  "salida":      { bg:"#EAFAF1", color:"#1D6A39", border:"#82E0AA", label:"Resultado" },
};

// Objeto de prioridades (FIJO, no cambiar)
const PRIORIDAD = {
  "Esencial":    { bg:"#FDEDEC", color:"#922B21", dot:"#E74C3C" },
  "Recomendado": { bg:"#FEF9E7", color:"#7D6608", dot:"#F39C12" },
  "A valorar":   { bg:"#F4F6F7", color:"#717D7E", dot:"#AEB6BF" },
};

// AREAS[] — array con los datos del mapa de procesos del lead
const AREAS = [ /* generado por la skill */ ];

// FUNCIONALIDADES[] — array con los módulos y funcionalidades del lead
const FUNCIONALIDADES = [ /* generado por la skill */ ];
```

---

## Naming del archivo de salida

```
brief_[org_slug]_[YYYYMMDD].html

Ejemplos:
  brief_colegio_profesional_20260310.html
  brief_clinica_dental_20260310.html
  brief_cooperativa_agricola_20260310.html
```

`org_slug` = nombre_org en minúsculas, sin tildes, espacios → guión bajo, máx 4 palabras.

---

## Checklist de calidad antes de guardar

- [ ] El nombre de la organización aparece en el nav y en los subtítulos
- [ ] El número de áreas, pasos e integraciones en el subtítulo es correcto
- [ ] Los chips del ecosistema reflejan los sistemas encontrados en la investigación
- [ ] Cada área tiene entre 6 y 9 pasos con tipos variados
- [ ] Cada área tiene al menos 1 integración y 2 fricciones concretas
- [ ] Los acordeones de funcionalidades abren/cierran correctamente
- [ ] Solo un acordeón abierto a la vez
- [ ] El detalle de área muestra flujo completo con línea conectora
- [ ] El botón "Volver" funciona y oculta el detalle
- [ ] El HTML es autocontenido (sin peticiones a servidores propios)
- [ ] Funciona sin conexión a internet (salvo Google Fonts)
