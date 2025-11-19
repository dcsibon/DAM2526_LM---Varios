
# Cómo usar fuentes en una página web

Cuando se diseña una página web, uno de los aspectos más importantes es elegir correctamente las fuentes tipográficas. 
En CSS existen varias formas de incorporar fuentes, dependiendo de dónde se encuentren y cómo queremos que se carguen.

A continuación se explican todas las opciones, desde las más básicas hasta las más avanzadas.

---

## 1. **Fuentes instaladas en el sistema (web-safe)**

Son las fuentes que ya vienen instaladas en Windows, Mac o Linux, como por ejemplo:

* Arial
* Verdana
* Times New Roman
* Georgia
* Courier New

Para usarlas solo hay que indicar su nombre:

```css
body {
  font-family: Arial, sans-serif;
}
```

> Siempre se recomienda añadir una **fuente de respaldo**, como `sans-serif`, `serif` o `monospace`, para garantizar compatibilidad.

---

## 2. **Fuentes locales dentro del proyecto (`@font-face`)**

Si se dispone de un archivo de fuente (por ejemplo `.woff2` o `.ttf`), puede cargarse directamente desde la carpeta del proyecto usando `@font-face`.

```css
@font-face {
  font-family: "MiFuente";
  src: url("fonts/MiFuente-Regular.woff2") format("woff2");
  font-weight: 400;
}
```

Uso posterior:

```css
body {
  font-family: "MiFuente", sans-serif;
}
```

Este método es útil cuando se necesita una fuente personalizada que no existe en Google Fonts o cuando debe funcionar sin conexión a Internet.

---

## 3. **Fuentes externas desde un servidor con `@font-face`**

También pueden cargarse fuentes desde una URL externa si apunta al archivo real de la fuente:

```css
@font-face {
  font-family: "OpenSansCustom";
  src: url("https://cdn.jsdelivr.net/npm/@fontsource/open-sans/files/open-sans-latin-400-normal.woff2")
       format("woff2");
  font-weight: 400;
}
```

Esto es válido siempre que:

* La URL sea estable.
* El servidor permita el acceso sin errores CORS.

---

## 4. **Google Fonts (método más usado hoy en día)**

Google Fonts es la forma más sencilla de incluir fuentes externas en una web. El navegador descarga la fuente desde los servidores de Google.

### Método recomendado: etiqueta `<link>` en el `<head>`

```html
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans:wght@400;700&display=swap" rel="stylesheet">
```

Uso:

```css
body {
  font-family: "Noto Sans", sans-serif;
}
```

### ¿Qué significa `wght@400;700`?

* `400` → peso normal
* `700` → negrita

Solo se descargarán esos pesos.

### ¿Qué hace `preconnect`?

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

> Acelera la descarga preparando la conexión, pero **no carga la fuente**.

---

## 5. **Uso de `@import` (menos recomendado)**

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans&display=swap');
```

Este método funciona, pero es más lento y Google desaconseja su uso.

---

## 6. **Fuentes variables (Variable Fonts)**

Algunas fuentes incluyen múltiples variaciones (peso, inclinación, anchura) en un único archivo.

```css
font-variation-settings: "wght" 600, "wdth" 90;
```

Permiten mayor flexibilidad sin descargar múltiples archivos.

---

## 7. **Buenas prácticas al definir fuentes**

### ✔ 1. Añadir siempre varias fuentes de respaldo

```css
font-family: "Roboto", "Segoe UI", Arial, sans-serif;
```

### ✔ 2. Preferir formatos modernos (`.woff2`)

Son más ligeros y rápidos.

### ✔ 3. Descargar solo los pesos necesarios

Evita cargar fuentes innecesarias.

### ✔ 4. Preferir `<link>` antes que `@import`

Proporciona mejor rendimiento.

---

## 8. **Resumen final**

| Método                       | ¿Qué es?                     | Ventajas                     | Inconvenientes                 |
| ---------------------------- | ---------------------------- | ---------------------------- | ------------------------------ |
| Fuentes del sistema          | Fuentes ya instaladas        | Rápidas y sin descargas      | Estilo limitado                |
| `@font-face` local           | Archivos dentro del proyecto | Control total                | Aumenta el tamaño del proyecto |
| `@font-face` con URL externa | Descarga desde un CDN        | No requiere archivos locales | Depende del servidor           |
| Google Fonts                 | Fuentes alojadas en Google   | Fácil, rápido, optimizado    | Requiere conexión a Internet   |
| `@import`                    | Carga fuentes desde el CSS   | Simple                       | Más lento, no recomendado      |
