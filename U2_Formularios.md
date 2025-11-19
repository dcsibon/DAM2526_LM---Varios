## 1. Qué es un formulario en HTML

Un **formulario** (`<form>`) es un contenedor que permite **recoger datos del usuario**
y **enviarlos a un servidor o procesarlos localmente** mediante un lenguaje como JavaScript o PHP.

📘 En resumen:

> Un formulario HTML define los **campos de entrada**, los **botones** y la **forma de enviar los datos**.

---

## 2. Estructura básica de un formulario

```html
<form action="/procesar.php" method="post">
  <label for="nombre">Nombre:</label>
  <input type="text" id="nombre" name="nombre">
  
  <input type="submit" value="Enviar">
</form>
```

| Elemento   | Descripción                                            |
| ---------- | ------------------------------------------------------ |
| `<form>`   | Contenedor principal del formulario.                   |
| `action`   | URL o recurso al que se envían los datos.              |
| `method`   | Método HTTP: `get` (visible en URL) o `post` (oculto). |
| `<input>`  | Campo de entrada de datos.                             |
| `<label>`  | Etiqueta descriptiva asociada a un campo (`for="id"`). |
| `<button>` | Botón de envío o acción.                               |

---

## 3. Atributos más importantes de `<form>`

| Atributo       | Descripción                                                       |
| -------------- | ----------------------------------------------------------------- |
| `action`       | Dirección (URL o script) que procesará los datos.                 |
| `method`       | Método de envío: `get` o `post`.                                  |
| `target`       | Dónde abrir la respuesta (`_self`, `_blank`, etc.).               |
| `enctype`      | Tipo de codificación (`multipart/form-data` para subir archivos). |
| `autocomplete` | Activa o desactiva la autocompletación.                           |

---

## 4. Tipos de campos `<input>` en HTML5

HTML5 amplió muchísimo las posibilidades del elemento `<input>`.
Hoy existen **más de 20 tipos**, aunque los más útiles y compatibles son los siguientes:

| Tipo (`type`)    | Descripción                           | Ejemplo visual                                |
| ---------------- | ------------------------------------- | --------------------------------------------- |
| `text`           | Campo de texto libre                  | `<input type="text">`                         |
| `password`       | Campo de contraseña                   | `<input type="password">`                     |
| `email`          | Valida formato de correo              | `<input type="email">`                        |
| `number`         | Acepta solo números                   | `<input type="number" min="0" max="10">`      |
| `date`           | Selector de fecha                     | `<input type="date">`                         |
| `time`           | Selector de hora                      | `<input type="time">`                         |
| `datetime-local` | Fecha y hora locales                  | `<input type="datetime-local">`               |
| `month`          | Selector de mes                       | `<input type="month">`                        |
| `week`           | Selector de semana                    | `<input type="week">`                         |
| `url`            | Valida formato de enlace              | `<input type="url">`                          |
| `tel`            | Campo de teléfono                     | `<input type="tel">`                          |
| `search`         | Campo de búsqueda (diseño optimizado) | `<input type="search">`                       |
| `range`          | Deslizador numérico                   | `<input type="range" min="0" max="100">`      |
| `color`          | Selector de color                     | `<input type="color">`                        |
| `checkbox`       | Casilla de verificación               | `<input type="checkbox">`                     |
| `radio`          | Opción única entre varias             | `<input type="radio" name="sexo" value="H">`  |
| `file`           | Subida de archivos                    | `<input type="file" accept=".jpg,.png">`      |
| `hidden`         | Campo oculto (no visible)             | `<input type="hidden" name="id" value="123">` |
| `submit`         | Envía el formulario                   | `<input type="submit" value="Enviar">`        |
| `reset`          | Restablece los campos                 | `<input type="reset" value="Borrar">`         |
| `button`         | Botón sin acción (para scripts)       | `<input type="button" value="Click">`         |

---

## 5. Otros elementos habituales en formularios

| Elemento     | Descripción                             | Ejemplo                                                                          |
| ------------ | --------------------------------------- | -------------------------------------------------------------------------------- |
| `<textarea>` | Campo de texto multilínea               | `<textarea rows="4" cols="40"></textarea>`                                       |
| `<select>`   | Menú desplegable                        | `<select><option>Opción 1</option></select>`                                     |
| `<optgroup>` | Agrupa opciones dentro de un `<select>` | `<optgroup label="Frutas">...</optgroup>`                                        |
| `<datalist>` | Ofrece autocompletado (HTML5)           | `<input list="frutas"><datalist id="frutas"><option>Manzana</option></datalist>` |
| `<fieldset>` | Agrupa campos relacionados              | `<fieldset><legend>Datos personales</legend>…</fieldset>`                        |
| `<legend>`   | Título del grupo de campos              | (Dentro de `<fieldset>`)                                                         |
| `<output>`   | Muestra resultados calculados           | `<output name="resultado"></output>`                                             |
| `<progress>` | Barra de progreso                       | `<progress value="70" max="100"></progress>`                                     |
| `<meter>`    | Indicador de medida                     | `<meter value="0.7">70%</meter>`                                                 |

---

## 6. Validación nativa en HTML5

HTML5 añadió **validaciones automáticas** en los formularios sin necesidad de JavaScript.

Ejemplo:

```html
<form>
  <input type="email" required placeholder="Introduce tu correo">
  <input type="number" min="1" max="10" required>
  <input type="submit" value="Enviar">
</form>
```

| Atributo      | Descripción                                 |
| ------------- | ------------------------------------------- |
| `required`    | Campo obligatorio                           |
| `min` / `max` | Rango de valores numéricos o fechas         |
| `pattern`     | Expresión regular personalizada             |
| `maxlength`   | Número máximo de caracteres                 |
| `step`        | Incrementos válidos para `number` o `range` |
| `placeholder` | Texto de ayuda dentro del campo             |

💡 El navegador mostrará automáticamente mensajes de error si los datos no cumplen el formato.

---

## 7. Ejemplo completo y moderno de formulario HTML5

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Formulario de contacto</title>
</head>
<body>
  <h2>Formulario de contacto</h2>
  <form action="/enviar.php" method="post" autocomplete="on">
    <fieldset>
      <legend>Datos personales</legend>
      <label for="nombre">Nombre:</label>
      <input type="text" id="nombre" name="nombre" required>

      <label for="email">Correo:</label>
      <input type="email" id="email" name="email" placeholder="ejemplo@correo.com" required>
    </fieldset>

    <fieldset>
      <legend>Preferencias</legend>
      <label for="color">Color favorito:</label>
      <input type="color" id="color" name="color">

      <label for="fecha">Fecha de contacto:</label>
      <input type="date" id="fecha" name="fecha">
    </fieldset>

    <input type="submit" value="Enviar">
    <input type="reset" value="Borrar">
  </form>
</body>
</html>
```

---

## 8. En resumen

| Categoría              | Elementos más usados en HTML5                     |
| ---------------------- | ------------------------------------------------- |
| **Contenedor**         | `<form>`                                          |
| **Texto**              | `<input type="text">`, `<textarea>`               |
| **Selección**          | `<select>`, `<option>`, `<datalist>`              |
| **Elección múltiple**  | `<checkbox>`, `<radio>`                           |
| **Fecha y hora**       | `date`, `time`, `datetime-local`, `month`, `week` |
| **Multimedia y color** | `file`, `color`, `range`                          |
| **Botones**            | `submit`, `reset`, `button`                       |
| **Accesibilidad**      | `<label>`, `placeholder`, `required`              |
| **Agrupación**         | `<fieldset>`, `<legend>`                          |
| **Resultado**          | `<output>`, `<progress>`, `<meter>`               |



* Los formularios HTML5 son la principal vía para **interactuar con el usuario y enviar datos al servidor**.
* HTML5 añadió **nuevos tipos de campos**, validación automática y elementos interactivos.
* Su uso correcto mejora la **usabilidad**, la **accesibilidad** y reduce la necesidad de código JavaScript adicional.
* Un buen formulario combina estructura semántica (`<label>`, `<fieldset>`) con validación (`required`, `pattern`, etc.) y accesibilidad.

---
