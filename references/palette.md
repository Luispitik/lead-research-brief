# Paleta de Colores — Brief Investigación Propuesta

## Paleta principal (8 colores para 8 áreas/módulos)

Usar en orden para las áreas del mapa. Si hay más de 8 áreas, repetir con variaciones.

| Índice | Nombre       | Color HEX | Light HEX | Uso sugerido                        |
|--------|-------------|-----------|-----------|-------------------------------------|
| 1      | Navy Blue   | #1B6CA8   | #D6EAF8   | Gestión principal, administración   |
| 2      | Teal        | #0E7C7B   | #D1F2EB   | Comunicaciones, notificaciones      |
| 3      | Purple      | #6C3483   | #F4ECF7   | Turno, designaciones, asignaciones  |
| 4      | Amber       | #B7770D   | #FEF9E7   | Cobros, facturación, aranceles      |
| 5      | Dark Purple | #7D3C98   | #F5EEF8   | Custodia, depósitos, activos        |
| 6      | Green       | #1D6A39   | #EAFAF1   | Servicios públicos, gratuito        |
| 7      | Navy Light  | #1A5276   | #D6EAF8   | Formación, RRHH, capacitación       |
| 8      | Dark Navy   | #2C3E50   | #F2F3F4   | Gobernanza, dirección, cumplimiento |

## Colores de sistema — cromo del brief

Este es el **cromo del brief**: la identidad de quien firma el entregable. Los valores de
abajo son un **default neutro y editorial**; si tienes marca propia, sustitúyelos por la
tuya de una sola vez aquí y en `references/html_template_guide.md`.

```
--cream:       #F7F3EA   (fondo general, neutro cálido)
--white:       #FFFFFF   (fondo tarjetas)
--navy:        #0A1232   (tinta — nav, títulos principales)
--text:        #0A1232   (tinta — texto body)
--muted:       #6E6759   (piedra — texto secundario)
--border:      #DCD4C2   (filete — bordes y separadores)
--gold:        #2020FF   (ÚNICO acento, barra decorativa. El nombre de la variable es
                          histórico: el valor ya no es dorado)
--red:         #B0453C   (alerta — fricciones. SIEMPRE con etiqueta de texto)
--red-light:   #ECE5D6   (arena — fondo de chips de fricción, neutro)
```

**Regla 90 · 9 · 1**: ≈90% superficie neutra cálida · ≈9% tinta · ≈1% acento como gesto.
El acento se percibe caro porque es escaso: si una página parece colorida, hay que
**quitar** acento, no añadirlo.

El nombre de la variable `--gold` se conserva para no romper las plantillas que ya la
referencian. Cambia su valor, no su nombre.

---

## Dos escalas de esta skill que NO son marca — no las sustituyas

Antes de "arreglar" un color de este fichero, comprueba en cuál de los dos grupos cae.

**1. La paleta de 8 áreas y las escalas de tipo de paso / prioridad** (arriba y abajo)
codifican **información dentro del mapa**, no identidad. Se conservan a propósito. Lo que
sí es obligatorio es que **cada área y cada paso lleve su etiqueta de texto**: el color no
puede ser el único portador del significado, porque el brief tiene que leerse igual
fotocopiado en blanco y negro.

**2. La paleta por sector de `app_demo_guide.md` es la marca DEL CLIENTE**, no la tuya.
La demo-app se pinta con los colores del cliente (extraídos de su web, o el fallback por
sector). Pintarla con el cromo del brief haría que todas las demos parecieran tuyas, que
es justo lo contrario de lo que busca esa pieza. **No tocar.**

## Tipos de paso — colores (fijos)

```
entrada:     bg:#EBF5FB  color:#1A5276  border:#AED6F1  label:"Entrada"
proceso:     bg:#FDFEFE  color:#2C3E50  border:#D5D8DC  label:"Proceso"
decisión:    bg:#FEFBE8  color:#7D6608  border:#F9E79F  label:"Decisión"
integración: bg:#E8F8F5  color:#1D6A39  border:#A9DFBF  label:"Integración"
salida:      bg:#EAFAF1  color:#1D6A39  border:#82E0AA  label:"Resultado"
```

## Prioridades de funcionalidades — colores (fijos)

```
Esencial:    bg:#FDEDEC  color:#922B21  dot:#E74C3C
Recomendado: bg:#FEF9E7  color:#7D6608  dot:#F39C12
A valorar:   bg:#F4F6F7  color:#717D7E  dot:#AEB6BF
```
