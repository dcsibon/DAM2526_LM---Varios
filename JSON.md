# JSON: Formato de Intercambio de Datos

## 1. Introducción

* **JSON** significa *JavaScript Object Notation*.
* Nació en el mundo web (JavaScript) a principios de los 2000, como una forma ligera de intercambiar datos en aplicaciones web usando JavaScript.
* Hoy lo usan casi todos los lenguajes de programación.
* Es un **formato ligero de texto plano** para representar datos estructurados, pensado para que sea **fácil de leer y escribir por humanos** y **fácil de procesar por máquinas**.
* Compite con **XML**, que fue durante muchos años el formato estándar de intercambio, pero JSON se ha impuesto en la mayoría de contextos modernos por su simplicidad.
* **Usos más comunes hoy**:

  * **APIs REST** → casi todos los servicios web devuelven JSON.
  * **Aplicaciones móviles** → Android/iOS lo usan para comunicarse con servidores.
  * **Bases de datos NoSQL** como MongoDB o CouchDB.
  * **Archivos de configuración** modernos (`package.json`, `composer.json`, etc.).

---

## 2. Reglas de JSON

Para que un archivo JSON sea **válido**, debe cumplir estas reglas:

1. **No existe prólogo**
   No hace falta indicar versión ni codificación. JSON siempre es texto plano UTF-8 (por defecto). 
   
   El propio formato se reconoce por la extensión del archivo `.json` y por el **MIME type** `application/json` cuando se transmite en la web.
   Por eso todos los ficheros JSON empiezan directamente con `{` o `[`.

2. **Elemento raíz único**
   Todo JSON debe comenzar con un único objeto `{ }` o array `[ ]`.
   Ejemplo:

   ```json
   { "universo":
     { ...
     }
   }
   ```

3. **Pares clave–valor**
   Un objeto es un conjunto de pares `"clave": valor`.

   * La **clave siempre es un string entre comillas dobles**.
   * El valor puede ser otro objeto, un array o un valor primitivo.

4. **Valores primitivos permitidos**

   * `"cadena"` → siempre con comillas dobles
   * `123` → número entero
   * `3.14` → número decimal (con punto)
   * `true` / `false` → booleanos en minúscula
   * `null` → valor nulo

5. **Arrays**
   Se declaran con corchetes `[ ]`.
   Los elementos se separan con comas.
   Ejemplo:

   ```json
   "planetas": ["Mercurio", "Venus", "Tierra"]
   ```

6. **Sin comentarios**
   JSON estándar no admite comentarios. Todo lo que escribas se interpreta como dato.

7. **Comas y comillas**

   * Nunca puede haber coma final en una lista u objeto.
   * Siempre se usan comillas dobles `" "` (no simples `' '`).

---

## 3. Ejemplos básicos

### Objeto simple

```json
{
  "nombre": "Tierra",
  "posicion": 3,
  "tipo": "rocoso",
  "tieneVida": true,
  "satelites": ["Luna"]
}
```

### Lista de valores primitivos

(Una lista de satélites expresados solo como nombres)

```json
{
  "satelites": [
    "Mimas",
    "Encelado",
    "Tetis",
    "Dione",
    "Rea",
    "Titán",
    "Hiperión",
    "Lapeto",
    "Foebe"
  ]
}
```

👉 Cada elemento del array es un **string**. Ideal cuando solo guardas un valor simple.

### Lista de objetos

(Una agenda donde cada contacto tiene varias propiedades)

```json
{
  "agenda": [
    {
      "nombre": "Ana",
      "telefono": "666111222",
      "activo": true
    },
    {
      "nombre": "Luis",
      "telefono": "666333444",
      "activo": false
    }
  ]
}
```

👉 Cada elemento del array es un **objeto** con varias propiedades. Útil cuando cada entidad necesita más información.

---

## 4. Comparación JSON vs XML

| Característica     | XML                                                   | JSON                                          |
| ------------------ | ----------------------------------------------------- | --------------------------------------------- |
| **Raíz**           | Un único elemento raíz                                | Un único objeto o array                       |
| **Estructura**     | Etiquetas `<tag>contenido</tag>`                      | Claves y valores `{ "clave": valor }`         |
| **Listas**         | Elementos repetidos `<item>…</item>`                  | Arrays `[ ]`                                  |
| **Atributos**      | `<planeta nombre="Marte" tipo="rocoso" />`            | `{ "nombre": "Marte", "tipo": "rocoso" }`     |
| **Tipos de datos** | Todo es texto (aunque represente números o booleanos) | Se distinguen: string, número, booleano, null |
| **Comentarios**    | `<!-- comentario -->`                                 | No se permiten                                |
| **Sintaxis**       | Verbosa, con apertura y cierre de etiquetas           | Compacta, clave-valor                         |
| **Usos actuales**  | Configuración, documentos, validación (XSD)           | APIs, web, móviles, bases de datos NoSQL      |

---

## 5. Ejemplo comparativo

**XML (agenda):**

```xml
<agenda>
  <contacto>
    <nombre>Ana</nombre>
    <telefono>666111222</telefono>
    <activo>true</activo>
  </contacto>
</agenda>
```

**JSON (equivalente):**

```json
{
  "agenda": [
    {
      "nombre": "Ana",
      "telefono": "666111222",
      "activo": true
    }
  ]
}
```

---

## 6. Validación

- **Bien formado**

   * Un archivo JSON debe cumplir estrictamente las reglas de sintaxis:

     * Claves con comillas dobles.
     * Comas solo entre elementos, nunca la última.
     * Arrays y objetos bien cerrados (`[]`, `{}`).
   * Si falla algo de esto → **no es JSON válido**.

- **Validación en el navegador**

   * Al abrir un `.json` en un navegador:

     * Si está correcto → se muestra estructurado (plegado/coloreado en Chrome/Firefox/Edge).
     * Si está mal formado → el navegador lo muestra como **texto plano**, sin error detallado (a diferencia de XML, que sí lanza error).

- **Cómo validar realmente**

   * Usar herramientas externas:

     * **Validadores online**: ej. [https://jsonlint.com](https://jsonlint.com).
     * **Editores/IDE** (VS Code, IntelliJ, etc.), que marcan errores de sintaxis.
     * **Programas** (JavaScript, Python, Java, etc.): al intentar cargar un JSON mal formado, lanzan un error de parsing.

- **JSON Schema (nivel avanzado)**

   * Al igual que XML tiene DTD o XML Schema, JSON tiene **JSON Schema**.
   * Sirve no solo para comprobar que es “bien formado”, sino también que cumple ciertas **reglas de contenido**:

     * Ejemplo: `"edad"` debe ser un número.
     * Ejemplo: `"activo"` debe ser booleano.

---

## 7. Conclusión

* JSON es más **ligero, sencillo y tipado** que XML.
* XML sigue siendo útil en contextos donde se requieren **documentos complejos o estándares antiguos**.
* JSON es el **formato predominante en el desarrollo actual** de aplicaciones web y móviles.
* Con arrays puedes representar tanto listas de valores primitivos (ej. satélites) como listas de objetos completos (ej. agenda de contactos).
