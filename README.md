# 🛒 Catálogo de Productos — Jerarquía CSS

Proyecto de la **Subactividad 1: Estructurar la jerarquía de estilos**  
Programa: Análisis y Desarrollo de Software  
Ficha: 3381732 
Instructor: John Freddy Becerra Castellanos  
Aprendiz: Juan David León

---

## 📖 Descripción

Página estática que simula un catálogo de productos tecnológicos.  
El objetivo es demostrar el dominio de los conceptos fundamentales de CSS:

- Herencia
- Cascada
- Especificidad
- Selectores combinados (etiqueta, clase, descendencia)

---

## 🧮 Cálculo de Especificidad

Cada selector CSS tiene un "peso" que determina qué regla gana cuando dos o más apuntan al mismo elemento.

| Tipo de selector | Peso      | Ejemplo           |
|------------------|-----------|-------------------|
| Etiqueta         | 1 punto   | `p`, `a`, `h2`    |
| Clase            | 10 puntos | `.btn-comprar`    |
| ID               | 100 puntos| `#btn-destacado`  |

### Ejemplos del proyecto

| Selector                   | Cálculo                    | Total |
|----------------------------|----------------------------|-------|
| `p`                        | 1                          | 1     |
| `article p`                | 1 + 1                      | 2     |
| `.precio`                  | 10                         | 10    |
| `header nav ul li a`       | 1+1+1+1+1                  | 5     |
| `.btn-comprar`             | 10                         | 10    |
| `#btn-destacado`           | 100                        | 100   |

### 🔥 Conflicto Cascada vs Especificidad

En la prueba se aplicó al enlace del segundo producto:

```html
<a href="#" class="btn-comprar" id="btn-destacado">Comprar</a>