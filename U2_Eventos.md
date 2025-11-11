# EVENTOS en HTML5 y su aplicación moderna con JavaScript

## 1. **Eventos de `<body>`**

### 🔹 `onload`

* **Qué hace:** Se dispara cuando el documento o recurso se ha cargado completamente.
* **Uso típico actual:** Ejecutar un script o inicializar una app cuando la página esté lista.
* **Ejemplo clásico (HTML directo):**

  ```html
  <body onload="inicializarPagina()">
  ```
* **Forma moderna (JavaScript separado):**

  ```js
  window.addEventListener("load", inicializarPagina);
  ```
* **Sí, sigue usándose**, aunque muchas veces sustituido por:

  ```js
  document.addEventListener("DOMContentLoaded", ...);
  ```

  Este último se dispara **antes**, cuando el DOM ya está listo (sin esperar a imágenes).

---

### 🔹 `onunload`

* **Qué hace:** Se ejecuta al abandonar la página (cierre, recarga o navegación).
* **Uso actual:** Muy limitado, porque los navegadores **restringen lo que se puede hacer** por seguridad y rendimiento.
* **Ejemplo clásico:**

  ```html
  <body onunload="alert('Adiós!')">
  ```
* **Ejemplo moderno (poco recomendable):**

  ```js
  window.addEventListener("unload", () => {
    console.log("Página cerrada");
  });
  ```
* ⚠️ **Hoy en día apenas se usa**, salvo para liberar recursos o guardar estado en aplicaciones SPA o frameworks tipo React/Vue (pero usando sus propios hooks, no el evento directamente).

---

## 🧾 2. **Eventos de formulario**

Estos siguen **plenamente vigentes y muy usados**. De hecho, son la base de la interacción con formularios en HTML5, validaciones, inputs, etc.

---

### 🔹 `onblur`

* **Qué hace:** Se dispara cuando un campo **pierde el foco** (el usuario hace clic fuera).
* **Uso actual:** Validar un campo individual cuando el usuario pasa al siguiente.
* **Ejemplo moderno:**

  ```js
  document.getElementById("email").addEventListener("blur", validarEmail);
  ```

---

### 🔹 `onchange`

* **Qué hace:** Se activa cuando un campo pierde el foco **y su valor cambió**.
* **Uso actual:** Común para `<input>`, `<select>`, `<textarea>`.
* **Ejemplo:**

  ```js
  document.getElementById("pais").addEventListener("change", actualizarProvincias);
  ```

---

### 🔹 `onfocus`

* **Qué hace:** Ocurre cuando un campo **recibe el foco** (clic o tabulador).
* **Uso actual:** Muy usado para resaltar o guiar al usuario.
* **Ejemplo:**

  ```js
  document.getElementById("nombre").addEventListener("focus", () => {
    console.log("Campo activo");
  });
  ```

---

### 🔹 `onreset`

* **Qué hace:** Se dispara cuando se hace clic en el botón “Reset” de un formulario.
* **Uso actual:** Poco frecuente, pero útil para advertir al usuario antes de borrar datos.
* **Ejemplo:**

  ```js
  document.querySelector("form").addEventListener("reset", confirmarReset);
  ```

---

### 🔹 `onselect`

* **Qué hace:** Se activa cuando el usuario selecciona texto dentro de un `<input>` o `<textarea>`.
* **Uso actual:** Raro, pero todavía válido (p. ej. para mostrar un contador de caracteres seleccionados).
* **Ejemplo:**

  ```js
  document.getElementById("comentario").addEventListener("select", mostrarSeleccion);
  ```

---

### 🔹 `onsubmit`

* **Qué hace:** Ocurre cuando se envía un formulario (al pulsar *Enter* o el botón *Enviar*).
* **Uso actual:** **Muy común**. Se usa para validar o impedir el envío hasta comprobar los datos.
* **Ejemplo:**

  ```js
  document.querySelector("form").addEventListener("submit", function(event) {
    if (!validarFormulario()) {
      event.preventDefault(); // evita el envío si hay errores
    }
  });
  ```

---

## 💡 Conclusión rápida

| Evento     | Actualidad HTML5 | Uso principal                                  |
| :--------- | :--------------- | :--------------------------------------------- |
| `onload`   | ✅ Muy usado      | Iniciar scripts o recursos al cargar la página |
| `onunload` | ⚠️ En desuso     | Liberar recursos (limitado)                    |
| `onblur`   | ✅ Vigente        | Validación de campos                           |
| `onchange` | ✅ Vigente        | Detección de cambios en inputs                 |
| `onfocus`  | ✅ Vigente        | Resaltar campos activos                        |
| `onreset`  | ⚙️ Ocasional     | Confirmar reseteo de formulario                |
| `onselect` | ⚙️ Poco usado    | Detectar selección de texto                    |
| `onsubmit` | ✅ Muy usado      | Validación y control del envío de formularios  |

---

## EJEMPLO DE USO DEL EVENTO `onload`

**Dos versiones**: primero la forma **clásica** (solo HTML, embebida en el atributo) y después la **moderna** (HTML + fichero `script.js` externo).

### **Versión 1 – Clásica (solo HTML)**

Uso directo del atributo `onload` dentro del `<body>`.
Esta forma es válida y comprensible para introducir el concepto de eventos.

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ejemplo onload clásico</title>
</head>
<body onload="mensajeBienvenida()">

  <h1>Bienvenido al sitio</h1>
  <p>Este ejemplo usa el evento <strong>onload</strong> directamente en el HTML.</p>

  <script>
    function mensajeBienvenida() {
      alert("La página se ha cargado correctamente. ¡Hola, alumno de DAM1!");
    }
  </script>

</body>
</html>
```

🔹 **Explicación:**

* El evento `onload` se ejecuta cuando todo el contenido del documento (HTML, imágenes, etc.) ha terminado de cargarse.
* Llama a la función `mensajeBienvenida()` definida en el bloque `<script>`.

---

### **Versión 2 – Moderna (HTML + JavaScript separado)**

Aquí se usa **JavaScript externo** y el **método `addEventListener()`**, que es la forma recomendada en HTML5.

**Archivo: `index.html`**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ejemplo onload moderno</title>
  <script src="script.js" defer></script>
</head>
<body>

  <h1>Bienvenido al sitio</h1>
  <p>Este ejemplo usa el evento <strong>load</strong> con <code>addEventListener()</code> desde un fichero externo.</p>

</body>
</html>
```

**Archivo: `script.js`**

```js
// Versión moderna: usar addEventListener en lugar de atributos HTML

window.addEventListener("load", function() {
  alert("La página se ha cargado correctamente. ¡Bienvenido desde script.js!");
});
```

🔹 **Explicación:**

**¿Qué es `defer`?**

El atributo **`defer`** se usa en la etiqueta `<script>` para **indicar al navegador que debe descargar el archivo JavaScript sin bloquear la carga del HTML**, y **ejecutarlo solo cuando el documento haya sido completamente analizado** (justo antes del evento `DOMContentLoaded`).

**Sintaxis**

```html
<script src="script.js" defer></script>
```

**¿Qué hace exactamente?**

1. **El navegador empieza a descargar el JS mientras sigue procesando el HTML.**
   (Así no se queda “esperando” al script).

2. **El script se ejecuta después de que todo el HTML haya sido leído y estructurado**,
   pero **antes de que se dispare el evento `DOMContentLoaded`**.

3. **El orden se respeta:** si hay varios scripts con `defer`, se ejecutan **en el orden en que aparecen**.

**🚫 Sin `defer` (comportamiento por defecto)**

Cuando no usas `defer`, el navegador **detiene el parseo del HTML** en el punto donde aparece `<script>` hasta que descarga y ejecuta el archivo.

Ejemplo clásico:

```html
<script src="script.js"></script>
```

👉 Esto puede hacer que la página tarde más en mostrarse, porque el HTML se “pausa” mientras se ejecuta el JS.

**✅ Con `defer`**

El navegador:

* **Descarga el script en paralelo** al HTML,
* **no bloquea la carga** del contenido,
* y **lo ejecuta al final**, cuando el DOM está listo.

```html
<script src="script.js" defer></script>
```

Así, los scripts pueden manipular el DOM con seguridad, sin necesidad de esperar manualmente al `onload` o al `DOMContentLoaded`.

**Ejemplo práctico**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ejemplo con defer</title>
  <script src="script.js" defer></script>
</head>
<body>
  <h1>Hola desde HTML</h1>
</body>
</html>
```

**script.js**

```js
console.log("El DOM ya está listo, se ejecuta después de analizar el HTML");
document.body.style.backgroundColor = "#e6f0ff";
```

---

### Diferencias clave

| Aspecto              | Versión clásica                            | Versión moderna                             |
| -------------------- | ------------------------------------------ | ------------------------------------------- |
| Ubicación del código | Dentro del HTML (`onload="..."`)           | En un archivo JS externo                    |
| Recomendación actual | ⚠️ Solo para ejemplos simples o didácticos | ✅ Recomendado (HTML limpio y reutilizable)  |
| Forma de ejecutar    | Directa con atributo                       | Escucha del evento con `addEventListener()` |
| Buenas prácticas     | Mezcla estructura y comportamiento         | Separa estructura (HTML) y lógica (JS)      |

---

## EJEMPLO DE USO DEL EVENTO `onblur`

A continuación, se muestra un **ejemplo sencillo, completo y moderno** usando
`document.getElementById("email").addEventListener("blur", validarEmail);`
para mostrar cómo funciona el evento **`blur`** al validar un campo de correo electrónico.

### **index.html**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Validación con evento blur</title>
  <script src="script.js" defer></script>
  <style>
    body {
      font-family: "Segoe UI", system-ui, sans-serif;
      background-color: #f4f6f8;
      text-align: center;
      padding-top: 60px;
    }

    form {
      background-color: white;
      width: 300px;
      margin: 0 auto;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }

    input[type="email"] {
      width: 90%;
      padding: 8px;
      margin-bottom: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 1rem;
    }

    #mensaje {
      font-size: 0.9rem;
      color: #d90429;
      min-height: 20px;
    }

    #mensaje.ok {
      color: #2b9348;
    }

    button {
      padding: 8px 16px;
      border: none;
      border-radius: 4px;
      background-color: #0d3b66;
      color: white;
      font-size: 1rem;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <form>
    <h2>Validación de correo</h2>
    <label for="email">Correo electrónico:</label><br>
    <input type="email" id="email" placeholder="usuario@ejemplo.com">
    <div id="mensaje"></div>
    <button type="submit">Enviar</button>
  </form>

</body>
</html>
```

### **script.js**

```js
// Al perder el foco (evento "blur"), se valida el contenido del campo email
document.getElementById("email").addEventListener("blur", validarEmail);

function validarEmail() {
  const emailInput = document.getElementById("email");
  const mensaje = document.getElementById("mensaje");
  const email = emailInput.value.trim();

  // Expresión regular básica para validar un correo
  const patron = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

  if (email === "") {
    mensaje.textContent = "El campo no puede estar vacío.";
    mensaje.classList.remove("ok");
  } else if (!patron.test(email)) {
    mensaje.textContent = "Introduce un correo válido (ej: usuario@dominio.com)";
    mensaje.classList.remove("ok");
  } else {
    mensaje.textContent = "Correo válido ✅";
    mensaje.classList.add("ok");
  }
}
```

### Explicación resumida

| Elemento                                         | Qué hace                                                  |
| ------------------------------------------------ | --------------------------------------------------------- |
| `addEventListener("blur", validarEmail)`         | Escucha cuando el campo pierde el foco.                   |
| `emailInput.value.trim()`                        | Obtiene el texto introducido sin espacios.                |
| Expresión regular `/^[^\s@]+@[^\s@]+\.[^\s@]+$/` | Verifica la estructura típica de un correo electrónico.   |
| Cambia el contenido de `#mensaje`                | Muestra el resultado visualmente al usuario.              |
| Uso de `defer`                                   | Asegura que el script se ejecute una vez cargado el HTML. |

### Comportamiento

1. EScribimos un correo en el campo.
2. Cuando sale del campo (clic fuera o tabulador) → se dispara `blur`.
3. Se muestra un mensaje de validación justo debajo del input.

---

### Explicación detallada

**1. Conectar JavaScript con el HTML**

```js
document.getElementById("email").addEventListener("blur", validarEmail);
```

* `document` → representa la página HTML cargada en el navegador.
* `getElementById("email")` → busca en el HTML el elemento que tenga `id="email"`.

  * En tu HTML tienes:

    ```html
    <input type="email" id="email">
    ```

    Así que esto encuentra ese `<input>`.

* `addEventListener("blur", validarEmail)`:

  * `addEventListener` significa: “escucha cuando pase algo”.
  * `"blur"` es el nombre del evento: sucede cuando el campo **pierde el foco** (cuando el usuario hace clic fuera o pulsa TAB).
  * `validarEmail` es el **nombre de la función** que queremos ejecutar cuando eso ocurra.

**2. Qué es una función**

```js
function validarEmail() {
  // ... código ...
}
```

* `function` → palabra clave para definir una función.
* `validarEmail` → nombre que le ponemos (como el nombre de una receta).
* `{ ... }` → entre llaves va el código que se ejecutará cuando llamemos a esa función.

Esta función es la que se ejecuta cuando salta el evento `"blur"` del campo email.

**3. Recuperar los elementos del HTML**

Dentro de la función:

```js
const emailInput = document.getElementById("email");
const mensaje = document.getElementById("mensaje");
const email = emailInput.value.trim();
```

* `const` → sirve para crear una constante (una variable cuyo nombre no vamos a cambiar).
* `emailInput` → aquí guardamos el elemento `<input id="email">`.
* `mensaje` → aquí guardamos el elemento `<div id="mensaje">`, que es donde mostraremos el texto de error o éxito.
* `emailInput.value` → es el **texto que el usuario ha escrito** en el campo.
* `.trim()` → quita espacios en blanco al principio y al final (por si alguien escribe `"  correo@x.com  "`).

**4. La regla para saber si es un email**

```js
const patron = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
```

* Es una **expresión regular**: una especie de “plantilla” para comprobar si un texto tiene formato de correo.
* No hace falta que sepais **regex** todavía. Sin tecnicismos, podemos explicarlo así:

> “Esta línea define una regla básica: tiene que haber texto antes de la @, una @, más texto, un punto y más texto después del punto.”

En modo muy simplificado:
`algo@algo.algo`

El método `patron.test(email)` devuelve:

* `true` → si parece un correo válido.
* `false` → si no tiene forma de correo.

**5. Comprobar los casos (estructura if / else)**

Aquí decidimos qué mensaje mostrar según lo que ha escrito el usuario.

```js
if (email === "") {
  mensaje.textContent = "El campo no puede estar vacío.";
  mensaje.classList.remove("ok");
} else if (!patron.test(email)) {
  mensaje.textContent = "Introduce un correo válido (ej: usuario@dominio.com)";
  mensaje.classList.remove("ok");
} else {
  mensaje.textContent = "Correo válido ✅";
  mensaje.classList.add("ok");
}
```

**a) `if (email === "")`**

* Si no ha escrito nada:

  * `mensaje.textContent` → cambia el texto que aparece en `<div id="mensaje">`.
  * `classList.remove("ok")` → por si antes estaba en verde, le quitamos la clase “ok”.

**b) `else if (!patron.test(email))`**

* `patron.test(email)` comprueba si el correo cumple la regla.
* `!` significa “no”.
* O sea: “si el correo **NO** cumple el formato correcto...”

  * Mostramos un mensaje de error.
  * Quitamos la clase “ok”.

**c) `else`**

* Si no está vacío **y** cumple el patrón:

  * Mostramos `"Correo válido ✅"`.
  * `mensaje.classList.add("ok")` → añade la clase CSS “ok” para ponerlo en verde (como definimos en el CSS).

**6. Relación con el CSS**

En el HTML tenéis algo como:

```css
#mensaje {
  font-size: 0.9rem;
  color: #d90429;   /* rojo por defecto */
  min-height: 20px;
}

#mensaje.ok {
  color: #2b9348;   /* verde cuando está bien */
}
```

* Cuando `classList.add("ok")`, el texto pasa a verde.
* Cuando `classList.remove("ok")`, vuelve al estilo de error.

**Resumen del comportamiento de este código:**

* “Cuando salimos del campo de email, este código mira lo que hemos escrito.
* Si está vacío → error.
* Si no tiene forma de correo → error.
* Si parece correcto → mensaje en verde.
* Todo esto se hace sin recargar la página y sin que nosotros tengamos que pulsar ningún botón.”

---


