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

## Hallazgos: Pseudoclases y Pseudoelementos

**(1) Diferencia funcional entre una pseudoclase y un pseudoelemento:**
Las **pseudoclases** (como `:hover`, `:active`, `:focus`) se usan para aplicar estilos a un elemento basándose en un **estado o evento** (cuando el usuario pasa el ratón, hace clic o navega con el teclado). Los **pseudoelementos** (como `::before` o `::after`) se usan para **inyectar contenido decorativo** (textos, iconos, líneas) en el DOM virtual, sin necesidad de escribir etiquetas HTML extra.

**(2) Importancia técnica de la pseudoclase `:focus`:**
Es vital para la **accesibilidad web**. Las personas que no usan ratón (por discapacidad motriz o preferencia) navegan usando la tecla `Tab`. El `:focus` con un `outline` visible les indica claramente en qué enlace o botón están posicionados, permitiéndoles navegar por el sitio sin perderse.

**(3) ¿Por qué inyectar decoraciones desde CSS (::before/::after)?**
Porque mantiene el HTML **semántico y limpio**. Si quisiéramos poner la etiqueta de "¡Oferta!" en el HTML, tendríamos que añadir un `<span>` vacío o extra en cada producto, lo cual ensucia el código. Al hacerlo con CSS, la etiqueta es puramente visual: si el día de mañana decidimos quitarla, solo borramos 8 líneas de CSS y el HTML queda intacto. Además, los lectores de pantalla para personas ciegas no leen los pseudoelementos, evitando que digan "Oferta" 4 veces seguidas.

## Hallazgos: Arquitectura BEM y Modularidad

**(1) ¿Qué significa BEM y cómo se escribe?**
BEM son las siglas de **Bloque, Elemento, Modificador**. Es una metodología para nombrar clases CSS. Se escribe así:
*   **Bloque:** El componente principal (ej. `.card`). Se usa una sola palabra.
*   **Elemento:** Una parte del bloque (ej. `.card__title`). Se une con doble guion bajo (`__`).
*   **Modificador:** Una variación del bloque o elemento (ej. `.card--destacada`). Se une con doble guion medio (`--`).

**(2) ¿Por qué dividir el CSS en varios archivos facilita el trabajo colaborativo?**
Porque si dos programadores están trabajando al mismo tiempo, uno puede estar editando `botones.css` mientras el otro edita `menu-lateral.css` sin que se generen conflictos en Git. Además, si hay un error en el diseño de las tarjetas, sabemos exactamente en qué archivo buscar sin tener que leer un documento de 1000 líneas.

**(3) ¿Cómo evita BEM la guerra de especificidad?**
BEM aplana el nivel de especificidad (peso 10) al usar casi exclusivamente **una sola clase** para seleccionar los elementos. Al eliminar selectores anidados complejos como `main section article h2`, evitamos que unas reglas pisen a otras por accidente. Si un estilo no se aplica, es fácil rastrearlo porque todo se maneja bajo el mismo nivel de peso.

## Hallazgos: Arquitectura Total con Flexbox

**(1) ¿Por qué fue crucial `min-height: 100vh` y `flex-direction: column` en el `.app-layout`?**
Porque `100vh` obliga al contenedor a medir exactamente el 100% de la altura de la ventana del navegador. Al combinarlo con `flex-direction: column`, creamos una columna donde el `header` y el `footer` toman el espacio que necesitan, y la propiedad `flex: 1` en el `.main-wrapper` hace que el contenido central "se estire" para ocupar todo el espacio sobrante. Esto garantiza que el pie de página siempre se quede pegado al fondo de la pantalla, incluso si hay pocos productos.

**(2) ¿Cómo la propiedad `gap` reemplazó el uso de márgenes laterales?**
Antes, para separar los enlaces del menú, teníamos que usar `margin-right` en cada `<li>` y luego borrar el margen del último elemento para que no se desalineara. Con Flexbox, `gap: 16px` aplica una separación matemática perfecta entre los hijos de un contenedor flexible, sin necesidad de tocar los márgenes individuales ni recurrir a pseudo-clases como `:last-child`.

**(3) ¿Cómo BEM, Custom Properties y Flexbox crearon una tarjeta resistente?**
La tarjeta ahora es un contenedor `display: flex; flex-direction: column;` con `height: 100%`. Al darle `flex-grow: 1` a la descripción (`.card__body`), le decimos al navegador: *"si a esta tarjeta le sobra espacio vertical porque el título de al lado es más corto, dale todo ese espacio a la descripción"*. Esto empuja el botón de compra hacia abajo, logrando que, sin importar cuánto texto tenga cada producto, todos los botones queden milimétricamente alineados en la misma línea horizontal.