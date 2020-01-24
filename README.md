> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)

> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc

# [WIP] Notas sobre APIs

## Contenido

- [API](https://github.com/undefinedschool/notes-apis#api)
- [REST](https://github.com/undefinedschool/notes-apis#rest)
  - [Propiedades de una API REST](https://github.com/undefinedschool/notes-apis#propiedades-de-una-api-rest)
- [CRUD](https://github.com/undefinedschool/notes-apis#crud)
- [API Key](https://github.com/undefinedschool/notes-apis#api-key)
- [Endpoint](https://github.com/undefinedschool/notes-apis#endpoint)
- [Verbos HTTP](https://github.com/undefinedschool/notes-apis#verbos-http)
- [HTTP Status Codes](https://github.com/undefinedschool/notes-apis#http-status-codes)
- [`path params` vs `query params` en una API REST](https://github.com/undefinedschool/notes-apis#path-params-vs-query-params-en-una-api-rest)
- [Ejercicio](https://github.com/undefinedschool/notes-apis#ejercicio)

---

## API

**A**pplication **P**rogramming **I**nterface), define una _interfaz_ con ciertas operaciones, que nos permiten interactuar con una aplicación hosteada en un servidor. 

Nos permite agregar una barrera de seguridad: el cliente no puede acceder directamente a la DB sino a través de la API. 

Una API expone datos y diferentes tipos de acciones que podemos realizar, a través de los _endpoints_, por ejemplo

- Información disponible
- Servicios
- Parámetros
- Formato de la respuesta

**Una API forma parte del backend de una aplicación** y es independiente de los lenguajes y plataformas que utilicemos.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

### Listas de APIs web disponibles para utilizar

- [RapidAPI](https://rapidapi.com/)
- [API List](https://apilist.fun/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

## REST

REST (**Re**presentational **S**tate **T**ransfer) es una _convención_ para desarrollar servicios web (APIs), basados en el protocolo HTTP. Vamos a llamar _APIs REST_ a las APIs que desarrollemos siguiendo estas convenciones.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

### Propiedades de una API REST

- Utilizamos **URLs para definir recursos**
- **`JSON`** como formato de intercambio
- Acciones basadas en los **verbos HTTP**
- Uso de los **status HTTP** (`200 - ok`, `404 - resource not found`, `500 - server error`, etc)
- **Stateless**: los datos del _cliente_ no se almacenan en el servidor entre requests. Cada request contiene toda la info necesaria para ser ejecutada, por lo que que ni el cliente ni el servidor necesitan recordar ningún estado previo.
- **Arquitectura cliente<->servidor:** hay una separación de responsabilidades entre el frontend (cliente) y el backend (server). Operan de forma independiente entre sí y ambos pueden ser reemplazados.
- **Cache**: la data que proviene del server puede ser _cacheada_ en el cliente, lo cual nos permite obtener mejoras de performance.

Ver más detalles en [Core Principles of RESTful API](https://www.moesif.com/blog/api-guide/getting-started-with-apis/#core-principles-of-restful-api)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

## CRUD

Una _API REST_ nos permite desarrollar servicios para crear, leer, actualizar o eliminar datos, conocidos como **CRUD operations** por sus siglas en inglés (**C**reate, **R**ead, **U**pdate, **D**elete).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

## API Key

Sirve para identificar al usuario/cliente que está realizando el request. Generalmente se utiliza para aplicar [_rate limiting_](https://apisyouwonthate.com/blog/what-is-api-rate-limiting-all-about) (limitar los recursos del servidor que podemos consumir de forma gratuita, por ejemplo bloqueando los requests después de cierta cantidad).

Para más info, ver [Use Web APIs](https://github.com/thejsway/thejsway/blob/master/manuscript/chapter22.md).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

## Endpoint

Un _endpoint_ de una API REST _expone un recurso o una colección de recursos_ para que sean consumidos. Un _endpoint_ incluye el tipo de acción (request) a realizar con el recurso (o la colección), la ruta y los parámetros necesarios. El tipo de acción está basado en los _verbos HTTP_ (`GET`, `POST`, `PUT`, `DELETE`, etc). Por ejemplo

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

### Ejemplos

**Request 1**

```
GET /api/customers
```

**Response 1**

```
[
 { "id": 1, "name": ...},
 { "id": 2, "name": ...},
 ...
]
```

**Request 2**

```
GET /api/customers/7
```

**Response 2**

```
{ "id": 7, "name": ...}
```

**Endpoints**

```
GET /api/customers
GET /api/customers/7
POST /api/customers
PUT /api/customers/1
DELETE /api/customers/2
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

## Verbos HTTP

- `GET`: Leer data de un recurso existente, sin modificarlo.
- `POST`: Crear un nuevo recurso en el server, usando la info enviada en el _payload_ del request. Por convención, cuando creamos un nuevo recurso, debemos retornar el objeto que lo representa en el `response`.
- `PUT`: Actualizar un recurso existente, usando la info enviada en el _payload_ del request. En el caso de que el recurso no exista, lo crea.
- `DELETE`: Eliminar un recurso existente.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

## HTTP Status Codes

Ver [httpstatuses.com](https://httpstatuses.com/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

## `path params` vs `query params` en una API REST

Ver [When do I use path params vs. query params in a RESTful API?](https://stackoverflow.com/a/31261026)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)

## Ejercicio

Vamos a crear una API REST con `Express`. La misma tendrá información sobre películas, almacenada en un array.

El formato de las películas será el siguiente:

```
movie = {
  "id": 1,
  "title": "Back to the Future",
  "year": 1985,
  "genre": "Science Fiction"
}
```

- Acá hay [ejemplos de películas para usar](https://www.imdb.com/list/ls009796553/) y acá tenés un [JSON con muchas más](https://gist.githubusercontent.com/nhsz/0005c21e6ebf9da151c900ff458f320e/raw/ebc9303155c71f1652adbca8f33887ee51a9eeaa/movies.json).
- El array de películas estará inicialmente vacío. 
- El `id` se calcula al agregar una nueva película (no forma parte del payload del request), según el orden (la primera tendrá `id=1`, la segunda `id=2`, etc).
- Utilizar el `Router` de `Express` para definir la lógica de routing en un módulo aparte, y setear `/api` como prefijo de todas las rutas. Utilizar el método [`route()`](http://expressjs.com/en/4x/api.html#router.route), para definir las rutas de una forma más declarativa. 
- Utilizar `nodemon` para desarrollar.
- En caso de necesitar _debuggear_ la aplicación, utilizar [esta guía](https://itnext.io/the-absolute-easiest-way-to-debug-node-js-with-vscode-2e02ef5b1bad).

### API Endpoints

- `GET /api/movies`: retorna el array de películas, en formato `JSON`.
- `GET /api/movies/:id`: retorna la película con el `id` correspondiente, en formato `JSON`. En el caso de que no exista, generar el error `"404 - The movie with the id {ID} was not found"` (donde ID es el parámetro utilizado) con `status code` 404 y pasarle el objeto `err` a `next`.
- `POST /api/movies`: agrega una nueva película, con la info especificada más arriba. Validar el `body` del request como se indica más abajo. Si es inválido, generar el error `"400 - Bad Request"` y pasarle el objeto `err` a `next`, sino, agregar la película correspondiente y retornar la info de la misma en el `response`.
- `PUT /api/movies/:id`: actualiza la info de una película (`title` ó `year`, el `id` no puede editarse). Para esto, primero debe buscarla por el `id` y si no existe, debe agregar la nueva película, con el `id` correspondiente.
- `DELETE /api/movies/:id`: elimina la película con el `id` correspondiente. Para esto, primero debe buscarla por el `id`, si no existe, generar el error `"404 - The movie with the id {ID} was not found"` (donde ID es el parámetro utilizado), y un `status code` 404 y pasarle el objeto `err` a `next`. Los `ids` de las películas restantes deberán ser actualizados para seguir siendo consecutivos, desde 1 a `n`, donde `n` es la cantidad de películas.
- `GET /api/movies/genres`: retorna la lista de géneros (sin repetir), correspondientes a las películas que tengamos
- `GET /api/movies/years`: retorna la lista de años (sin repetir), correspondientes a las películas que tengamos

### Query strings

- Si se utiliza el query string `?year=`, debe retornarse la lista de películas correspondientes a ese año, en formato `JSON`.
- Si se utiliza el query string `?genre=`, debe retornarse la lista de películas correspondientes a ese género, en formato `JSON`.
- Si se utilizan los query strings `?sortBy=title` ó `?sortBy=year` con el endpoint `GET /api/movies`, debe retornarse la lista de películas ordenada por año ó nombre, respectivamente.

En ambos casos, si no hay películas para mostrar, debe retornarse el array vacío `[]` (siempre como `JSON`).

### Validaciones

Utilizar el middleware [`express-validator`](https://express-validator.github.io/) para realizar las siguientes validaciones sobre el input (`body` del request)

- `title`: debe existir y tener al menos 2 caracteres, sino generar el error `movie title is required and should have minimum 2 characters.`, con `status code` 400 y pasarle el objeto `err` a `next`.
- `year`: debe ser un valor numérico entre 1800 y 2020, sino generar el error `movie year is required and should be a number between 1800 and 2020.`, con `status code` 400 y pasarle el objeto `err` a `next`.

### Middleware a utilizar

- `Router` de `Express`
- Error-handling middleware (ver detalles en [helpful-express-middleware](https://www.rithmschool.com/courses/node-express-fundamentals/helpful-express-middleware))
- [`express-validator`](https://express-validator.github.io/), para realizar las validaciones correspondientes
- [`morgan`](https://www.npmjs.com/package/morgan), para loguear en la terminal todos los _requests_ y _responses_ generados

[↑ Ir al inicio](https://github.com/undefinedschool/notes-apis#contenido)
