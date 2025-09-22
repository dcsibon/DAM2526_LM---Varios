## 📌 ¿Cuándo usar **atributos**?

1. **Metadatos** o propiedades de un elemento, es decir, información que lo **califica**.

   * Ejemplo:

     ```xml
     <pelicula id="P001" idioma="es">
         <titulo>Dune</titulo>
     </pelicula>
     ```

     Aquí `id` e `idioma` son características de la película.

2. **Valores cortos y simples**, que no necesitan estructura ni formato especial.

3. Cuando la información es **única y no repetible** para ese elemento.

4. Cuando se quiere usar como **clave** o referencia.

## 📌 Cuándo usar **subelementos**

1. **Datos de contenido** que forman parte de la información principal del documento.

   * Ejemplo:

     ```xml
     <pelicula>
         <titulo>Dune</titulo>
         <director>Denis Villeneuve</director>
     </pelicula>
     ```

2. **Información compleja o jerárquica**, que puede contener varios niveles, etiquetas anidadas o incluso listas.

3. Cuando el valor necesita **formato especial**, texto largo o caracteres especiales (parrafos, descripciones, etc.).

4. Cuando se espera que pueda haber **varias ocurrencias** de ese dato dentro del elemento.

   * Ejemplo: varios `<actor>` dentro de una `<pelicula>`.

## 📌 Regla práctica

* **Atributos → describen** (metadatos).
* **Elementos → contienen** (datos principales).

## 📌 Ejemplo comparativo

```xml
<!-- Usando atributos -->
<libro id="L001" idioma="es" publicado="2020">
    <titulo>Programación en XML</titulo>
</libro>

<!-- Usando subelementos -->
<libro>
    <id>L001</id>
    <idioma>es</idioma>
    <publicado>2020</publicado>
    <titulo>Programación en XML</titulo>
</libro>
```

Ambas formas son válidas, pero la primera es más ligera y describe mejor la semántica (los atributos son propiedades del libro, el título es el contenido principal).
