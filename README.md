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