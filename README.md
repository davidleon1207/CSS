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