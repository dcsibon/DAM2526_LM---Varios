
# FLEX y GRID

Cuando hacemos páginas web, los elementos (cajas, menús, fotos, textos…) no se colocan solos. Necesitamos una forma de organizarlos.

Hoy en día existen dos herramientas modernas para colocar elementos:

* **Flexbox** → Para colocar en **fila o en columna**
* **Grid** → Para colocar en **filas y columnas a la vez**

Son mucho más fáciles que las técnicas antiguas (tablas, floats…), y son lo que se usa en el mundo real.

---

## 🟦 PARTE 1 — FLEXBOX: Colocar elementos en una sola dirección

### 🧠 Idea clave en una frase

> **Flexbox sirve para organizar elementos en fila o en columna.**

Para activarlo:

```css
.container {
  display: flex;
}
```

Y ya está: Flexbox se pone en marcha.

---

### ¿Cómo decide Flexbox dónde coloca cada cosa?

Flexbox trabaja siempre con **dos ejes**:

#### ✔ Eje principal (main axis)

Es donde se colocan los elementos.

#### ✔ Eje secundario (cross axis)

Es perpendicular al principal.

### ¿Quién decide la dirección?

La propiedad:

```css
flex-direction
```

Si es `row` → fila → eje principal horizontal
Si es `column` → columna → eje principal vertical

---

## 🔳 Alineaciones importantes

#### `justify-content`

Alinea en el **eje principal**

#### `align-items`

Alinea en el **eje secundario**

### Explicación de **align-items** simplificada para alumnos

> **align-items mueve los elementos arriba, abajo o al centro según el EJE SECUNDARIO, pero SOLO si queda espacio disponible.**

Ejemplo con `flex-direction: row`:

* eje principal → horizontal
* eje secundario → vertical

Entonces:

```css
align-items: flex-start;  /* arriba */
align-items: center;      /* centrado vertical */
align-items: flex-end;    /* abajo */
align-items: stretch;     /* se estiran para rellenar verticalmente */
```

**Pero importante:**

Si el contenedor NO es más alto que los elementos, no notarás nada.
Porque **no habrá espacio que “rellenar” o donde moverlos**.

Esto lo explicarás tú en detalle en clase (lo dominas perfectamente).

---

## 🧪 Ejemplo práctico

#### HTML

```html
<div class="caja">
  <div>A</div>
  <div>B</div>
  <div>C</div>
</div>
```

#### CSS

```css
.caja {
  display: flex;
  height: 200px;
  background: #ddd;
  align-items: center; /* prueba start, center, end */
}
```

Cambiar `align-items` y ver cómo se mueven verticalmente.

---

## 🟧 PARTE 2 — GRID: Colocar elementos en filas y columnas

### 🧠 Idea clave en una frase

> **Grid sirve para crear estructuras en dos dimensiones: filas y columnas.**

Activarlo:

```css
.container {
  display: grid;
}
```

---

## 🔳 Crear columnas

```css
grid-template-columns: 1fr 1fr 1fr;
```

Esto crea 3 columnas iguales.

O con tamaños distintos:

```css
grid-template-columns: 200px 1fr 2fr;
```

---

## 🔳 Crear filas

```css
grid-template-rows: 100px auto 200px;
```

---

## 🔳 Hacer que un elemento ocupe varias columnas

```css
.item1 {
  grid-column: span 2;
}
```

---

## 🔳 Técnica más intuitiva: `grid-template-areas`

Permite “dibujar” layouts:

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr;
  grid-template-areas:
    "header header"
    "menu   main"
    "footer footer";
}

header { grid-area: header; }
nav    { grid-area: menu; }
main   { grid-area: main; }
footer { grid-area: footer; }
```

---

# 🌟 RESUMEN VISUAL

| Sistema     | Para qué sirve                         |
| ----------- | -------------------------------------- |
| **Flexbox** | Distribuir elementos en fila o columna |
| **Grid**    | Crear filas y columnas a la vez        |

---

# 🧪 Ejemplo muy simple (Grid)

### HTML

```html
<div class="grid">
  <div>1</div><div>2</div><div>3</div>
  <div>4</div><div>5</div><div>6</div>
</div>
```

### CSS

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```

---

## 🎮 JUEGOS RECOMENDADOS PARA APRENDER FLEX Y GRID

### 🐸 **1. Flexbox Froggy — para aprender Flexbox**

**[https://flexboxfroggy.com](https://flexboxfroggy.com)**

Ayudas a unas ranas a llegar a sus hojas usando propiedades de Flexbox.

Ideal para introducir:

* `justify-content`
* `align-items`
* `flex-direction`
* `flex-wrap`

Está en español y os recomiendo llegar al nivel 15.

---

### 🥕 **2. Grid Garden — para aprender Grid**

**[https://cssgridgarden.com](https://cssgridgarden.com)**

Riegas zanahorias utilizando:

* `grid-template-columns`
* `grid-template-rows`
* `grid-column`
* `grid-row`

Muy visual, ideal tras una introducción corta. Recomendable llegar al nivel 20.

---

### 🧨 **3. Flexbox Defense — Flexbox más avanzado**

**[https://flexboxdefense.com](https://flexboxdefense.com)**

Colocas cañones usando propiedades de Flexbox.
Es un *tower defense*, más divertido pero ligeramente más exigente.

Os lo recomiendo como actividad opcional o extra, para adquirir un nivel un poco más avanzado.

---
