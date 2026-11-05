# Catálogo de Productos — Jerarquía CSS

Subactividad 1: Estructurar la jerarquía de estilos (Selectores, herencia, cascada y especificidad).

## Cálculo de Especificidad

| Selector | Peso | Puntos |
|----------|------|--------|
| Etiqueta (`p`, `a`, `h2`) | 1 | 1 pt |
| Clase (`.btn-comprar`) | 10 | 10 pts |
| ID (`#btn-destacado`) | 100 | 100 pts |

### Ejemplos del proyecto

| Selector | Cálculo | Total |
|----------|---------|-------|
| `p` | 1 | 1 |
| `.precio` | 10 | 10 |
| `header nav ul li a` | 1+1+1+1+1 | 5 |
| `.btn-comprar` | 10 | 10 |
| `#btn-destacado` | 100 | 100 |

## Conflicto Cascada vs Especificidad

Se aplicó a un enlace: `class="btn-comprar"` e `id="btn-destacado"`.

En el CSS se declaró primero el ID (rojo, 100 pts) y luego la clase (naranja, 10 pts).
En pantalla el enlace se ve ROJO, demostrando que el ID aplasta a la clase
aunque la clase esté escrita después. La cascada solo habría ganado si ambas
reglas tuvieran el mismo peso.
/* DEMO TEMPORAL */
#btn-destacado { background-color: red; }
.btn-comprar   { background-color: orange; }

## Hallazgos: El Modelo de Caja

**1. Diferencia práctica entre Margin y Padding:**
El `padding` es el espacio "interno" de la caja (el oxígeno que separa el texto del borde de su propia tarjeta). El `margin` es el espacio "externo" (el campo de fuerza que empuja otras cajas lejos de ella). Si le pongo color de fondo a una caja, el `padding` se pinta de ese color; el `margin` siempre es transparente.

**2. ¿Por qué es obligatorio usar box-sizing: border-box?**
Porque por defecto, el navegador suma el ancho del `padding` y los bordes al ancho total del elemento. Si tengo un div de `width: 100%` y le agrego `padding: 20px`, el div se desborda de la pantalla. Con `border-box`, le decimos al navegador: *"si mido 100px, esos 100px incluyen todo (contenido, padding y borde)"*, evitando que la estructura se rompa.

**3. ¿Cómo afecta un margen grande a los hermanos?**
Si tengo dos tarjetas (hermanos) una debajo de la otra y le aplico un `margin-bottom: 50px` a la primera, esta empujará a la segunda tarjeta 50px hacia abajo. Si ambas tienen márgenes, los márgenes se "fusionan" (Margin Collapse) y se toma el valor más grande, no la suma de ambos.

## Hallazgos: Centralización de Identidad Visual y Espaciado

**(1) Lista completa de variables declaradas:**
* **Colores:** `--color-texto`, `--color-fondo-main`, `--color-fondo-aside`, `--color-fondo-footer`, `--color-blanco`, `--color-precio`, `--color-boton`, `--color-enlaces-footer`.
* **Tipografía:** `--fuente-principal` (Poppins).
* **Espaciados:** `--espaciado-caja` (20px), `--espaciado-menus` (15px), `--espaciado-boton` (5px 10px).

**(2) Ventaja de reutilizar medidas de margen y relleno:**
Antes de usar variables, si quería cambiar el aire de las tarjetas, tenía que modificar el `padding` en varias reglas. Ahora, al tener `--espaciado-caja: 20px`, puedo cambiar el diseño de todo el catálogo (header, tarjetas, aside, footer) modificando únicamente esa variable en la central `:root`. Esto asegura una proporción uniforme en toda la pantalla.

**(3) ¿Cómo previene colisiones visuales la centralización en `:root`?**
Porque elimina la "deuda técnica". Al no repetir valores hexadecimales (como `#1f2937`) o medidas (como `20px`) por todo el archivo, evito errores de tipeo. A medida que la hoja de estilos crece y se agregan más páginas, la centralización garantiza que todos los elementos compartan exactamente los mismos colores y medidas, sin que queden "parches" con estilos antiguos.