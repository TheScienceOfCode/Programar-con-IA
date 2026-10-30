---
title: "Lección 2: Entiende el backend de una API"
courseTitle: "Aprende a\nProgramar con IA"
language: es
objectives:
  - Entender qué ofrecen una API, HTTP y REST
  - Reconocer las piezas básicas de C# orientado a objetos
  - Comprender cómo el controlador usa EF Core para consultar y guardar tareas
  - Probar la API desde Swagger y modificar código pequeño
prerequisites:
  - Lección 1
  - Docker y un editor de código
---

# Lección 2 — Entiende el backend de una API

**Código:** https://github.com/TheScienceOfCode/Ejemplos-IA/tree/Todo-IA

**Formato:** una pantalla por cada `###`, con narración y escena visual. Las preguntas se hacen después de la narración.

**Criterio audiovisual:** lo que aparece entre el título de cada pantalla y `scene` es lo único que se narra. No narrar rutas, fragmentos de código, instrucciones de producción ni contenido de `scene` o `exercise`. La narración es texto hablado, sin formato Markdown. Los bloques visuales deben representar la idea, no limitarse a mostrar palabras sobre una diapositiva.

**Escenas:** `swagger-mock` representa la interfaz de Swagger con sus operaciones plegadas, botones Try it out/Execute, datos de entrada y respuestas. Es una simulación visual fiel a la API real, no una captura que afirme haber ejecutado peticiones. Si AutoTorial no tiene ese componente, crearlo o utilizar una grabación de Swagger real. `code` muestra únicamente el fragmento indicado del repositorio y resalta la parte señalada. Ninguna ruta de archivo debe convertirse en voz.

## Partes

### 1. ¿Qué es una API?

Una API, o interfaz de programación de aplicaciones, permite que se comuniquen dos programas de computador. En nuestro caso, el backend va a exponer una API para que el frontend la consuma. Esa API permitirá consultar información y realizar operaciones que terminarán con datos guardados o modificados en una base de datos.

```scene
id: what-is-api
type: visual
visual: timeline
plain: true
items:
  - icon: 🖥️
    label: Frontend
    detail: Muestra y recolecta información
  - icon: 🔌
    label: API
    detail: Reglas para comunicarse
  - icon: ⚙️
    label: Backend
    detail: Procesa la solicitud
  - icon: 💾
    label: Base de datos
    detail: Guarda o entrega los datos
```

### 2. Nuestro ejemplo: un tablero de tareas

Para el ejemplo de hoy vamos a construir el backend de un tablero de tareas pendientes. Queremos consultar y crear tareas, y moverlas entre tres estados: pendiente, en progreso y terminado. La API ofrecerá esas operaciones. Más adelante podremos crear una pantalla que las utilice.

```scene
id: task-board
type: visual
visual: task-board
items:
  - icon: ⏳
    label: Pendiente
    detail: Pending
    steps:
      - Comprar café
      - Revisar el correo
  - icon: 🛠️
    label: En progreso
    detail: InProgress
    steps:
      - Preparar la clase
  - icon: ✅
    label: Terminado
    detail: Done
    steps:
      - Enviar la factura
```

### 3. HTTP: peticiones y respuestas

#### La dirección

Cuando abrimos el navegador y vamos a una dirección, esa dirección suele tener una estructura. Empieza con http, que indica el protocolo de comunicación. Es algo muy técnico, pero es lo que permite que programas diferentes puedan comunicarse por internet. Después viene el lugar donde está el servidor y, al final, el recurso que queremos pedir.

```scene
id: url-anatomy
type: visual
visual: url-anatomy
steps:
  - "Reglas que permiten que programas diferentes se comuniquen por internet"
items:
  - icon: 🤝
    label: "http://"
    detail: Protocolo
    at: "Empieza con http"
  - icon: 🖥️
    label: "localhost:5080"
    detail: Servidor
    at: "Después viene el lugar"
  - icon: 📋
    label: "/api/tareas"
    detail: Recurso
    at: "al final, el recurso"
```

#### Petición y respuesta

Cuando el frontend necesita obtener información, envía una petición http al backend, que llega hasta la base de datos. El backend devuelve una respuesta a esa petición, y el frontend la procesa.

```scene
id: http-request-response
type: visual
visual: request-flow
steps:
  - "El frontend envía una petición HTTP"
  - "El backend consulta la base de datos"
  - "La base de datos entrega los datos"
  - "El backend devuelve una respuesta HTTP"
  - "El frontend procesa la respuesta"
stepAt:
  - "Cuando el frontend"
  - "que llega hasta"
  - "la base de datos"
  - "El backend devuelve"
  - "y el frontend la procesa"
items:
  - icon: 🖥️
    label: Frontend
  - icon: ⚙️
    label: Backend
  - icon: 💾
    label: Base de datos
```

### 4. Controladores: un ejemplo de hola mundo

```exercise
id: controller-memory
type: multiple-choice
prompt: "Si reiniciamos la aplicación, ¿qué pasa con los nombres guardados en la lista en memoria?"
choices:
  - "Desaparecen, porque no se guardaron en una base de datos"
  - "Se guardan automáticamente en SQLite"
  - "Pasan al frontend"
answer: 0
explanation: "Una lista en memoria vive mientras la aplicación está en marcha. Para conservar datos necesitamos persistirlos."
```

#### Un controlador de usuarios

Antes de usar nuestra aplicación de tareas, veamos un ejemplo muy pequeño. En una API, quien recibe las peticiones es un controlador: una clase que expone un recurso y tiene métodos que se ejecutan cuando llega una petición. Vamos a crear uno para usuarios. Guarda los nombres en una lista de textos y tiene un método para obtenerlos.

```scene
id: hello-controller
type: code
language: csharp
focus:
  - lines: [4]
    at: "quien recibe las peticiones"
  - lines: [2, 3, 4]
    at: "Vamos a crear uno para usuarios"
  - lines: [6]
    at: "Guarda los nombres"
  - lines: [8, 9, 10, 11, 12]
    at: "tiene un método para obtenerlos"
code: |-
  // Ejemplo didáctico: no está en el repositorio
  [ApiController]
  [Route("usuarios")]
  public class UsuariosController : ControllerBase
  {
      static List<string> usuarios = new();

      [HttpGet("obtener")]
      public List<string> Obtener()
      {
          return usuarios;
      }
  }
```

#### Crear y remover

Con otro método agregamos un nombre a la lista, y con otro lo quitamos. Cada método responde a una dirección distinta: obtener, crear y remover.

```scene
id: hello-controller-more
type: code
language: csharp
focus:
  - lines: [2, 3, 4, 5, 6]
    at: "Con otro método agregamos"
  - lines: [8, 9, 10, 11, 12]
    at: "y con otro lo quitamos"
  - lines: [2, 8]
    at: "Cada método responde a una dirección distinta"
code: |-
  // Ejemplo didáctico (continuación)
  [HttpPost("crear")]
  public void Crear(string nombre)
  {
      usuarios.Add(nombre);
  }

  [HttpPost("remover")]
  public void Remover(string nombre)
  {
      usuarios.Remove(nombre);
  }
```

#### Probando el controlador

Hagamos algunas peticiones. Creamos a Ana y luego a Luis. Al consultar, la lista tiene a los dos. Si quitamos a Ana, queda solo Luis. Pero fíjate dónde vive esa lista: en la memoria de la aplicación. Si la reiniciamos, los nombres desaparecen, porque no tenemos una base de datos que los guarde. Así vemos qué es un controlador, cómo expone un recurso, y por qué después necesitaremos persistir la información.

```scene
id: hello-requests
type: visual
visual: memory-list
items:
  - icon: 📤
    label: "POST /usuarios/crear?nombre=Ana"
    detail: Agrega a Ana
    at: "Creamos a Ana"
    steps: [Ana]
  - icon: 📤
    label: "POST /usuarios/crear?nombre=Luis"
    detail: Agrega a Luis
    at: "y luego a Luis"
    steps: [Ana, Luis]
  - icon: 📥
    label: "GET /usuarios/obtener"
    detail: Devuelve Ana y Luis
    at: "Al consultar"
    steps: [Ana, Luis]
  - icon: 📤
    label: "POST /usuarios/remover?nombre=Ana"
    detail: Quita a Ana
    at: "Si quitamos a Ana"
    steps: [Luis]
  - icon: 🔄
    label: Reiniciar la aplicación
    detail: La lista vuelve a estar vacía
    at: "Si la reiniciamos"
    steps: []
```

### 5. REST y RESTful

#### Convenciones

Existen ciertas convenciones sobre cómo organizar las API, y una de las más usadas es RESTful. En RESTful definimos recursos y, en vez de tener múltiples rutas para crear, consultar o remover, usamos los verbos http. Mira cómo estaba nuestro ejemplo: una ruta distinta para cada acción.

```scene
id: rest-before
type: visual
visual: swagger-mock
stage: method-map
header: "Una ruta por acción"
operations:
  - method: GET
    path: /usuarios/obtener
    caption: Obtener
  - method: POST
    path: /usuarios/crear
    caption: Crear
  - method: POST
    path: /usuarios/remover
    caption: Remover
```

#### Un recurso, varios verbos

Convirtamos el ejemplo. Ahora el recurso es usuarios, y una misma dirección sirve para todo. GET consulta la lista, POST agrega un usuario y DELETE lo quita. La dirección identifica el recurso, y el verbo indica la acción.

```scene
id: rest-after
type: visual
visual: swagger-mock
stage: method-map
header: "RESTful: un recurso, varios verbos"
operations:
  - method: GET
    path: /usuarios
    caption: Obtener
  - method: POST
    path: /usuarios
    caption: Crear
  - method: DELETE
    path: /usuarios/{nombre}
    caption: Remover
```

#### El mismo controlador, RESTful

Así queda el código. Los métodos son los mismos; lo que cambia son los atributos que conectan cada método con un verbo.

```scene
id: rest-controller
type: code
language: csharp
focus:
  - lines: [6, 9, 12]
    at: "Los métodos son los mismos"
  - lines: [5, 8, 11]
    at: "lo que cambia son los atributos"
code: |-
  // Ejemplo didáctico: el mismo controlador, RESTful
  [Route("usuarios")]
  public class UsuariosController : ControllerBase
  {
      [HttpGet]
      public List<string> Obtener() { ... }

      [HttpPost]
      public void Crear(string nombre) { ... }

      [HttpDelete("{nombre}")]
      public void Remover(string nombre) { ... }
  }
```

### 6. Métodos HTTP en nuestra API

Veamos esas convenciones en acción. GET sirve para consultar. POST, para crear una tarea nueva. PUT, para actualizarla, por ejemplo cuando pasa de pendiente a terminada. Y DELETE, para borrarla. Las direcciones nos dicen sobre qué tareas vamos a trabajar; el método nos dice qué queremos hacer.

```scene
id: rest-real-endpoints
type: visual
visual: swagger-mock
stage: method-map
header: "API de Tareas — endpoints reales"
show: "Vista Swagger con los cinco endpoints reales, cada método con su color distintivo. Al pasar de uno a otro resaltar método, dirección y acción. Explicar visualmente que {id} identifica una tarea."
operations:
  - method: GET
    path: /api/tareas
    caption: Listar todas
  - method: GET
    path: /api/tareas/{id}
    caption: Buscar una
  - method: POST
    path: /api/tareas
    caption: Crear
  - method: PUT
    path: /api/tareas/{id}
    caption: Actualizar
  - method: DELETE
    path: /api/tareas/{id}
    caption: Eliminar
```

```exercise
id: rest-check
type: multiple-choice
prompt: "Si una tarea ya existe y quieres cambiarla a terminada, ¿qué método HTTP usarías?"
choices:
  - "GET"
  - "PUT"
  - "POST"
answer: 1
explanation: "PUT actualiza una tarea existente."
```

### 7. Programación orientada a objetos

#### Una clase, un atributo y un método

Para entender el código necesitamos un concepto importante: la programación orientada a objetos. Organizamos el programa en clases, que son moldes para crear objetos. Veamos una clase genérica, que no hace nada. Puede tener atributos, también llamados propiedades: guardan datos, y se escriben con su tipo y su nombre. Y puede tener métodos: son acciones, y se escriben con el tipo que devuelven, su nombre y unos paréntesis. Lo que el método hace va dentro de las llaves.

```scene
id: oop-generic
type: code
language: csharp
focus:
  - lines: [2]
    at: "Organizamos el programa en clases"
  - lines: [4]
    at: "Puede tener atributos"
  - lines: [6]
    at: "Y puede tener métodos"
  - lines: [7, 8]
    at: "Lo que el método hace"
code: |-
  // Ejemplo genérico: una clase que no hace nada
  public class Ejemplo
  {
      public string Atributo { get; set; }

      public void Metodo()
      {
      }
  }
```

#### Una clase real: Tarea

Ahora una clase con sentido. Una tarea tiene un título y un estado. Esos son sus atributos o propiedades.

```scene
id: oop-tarea
type: code
language: csharp
focus:
  - lines: [1]
    at: "Ahora una clase con sentido"
  - lines: [3]
    at: "un título"
  - lines: [4]
    at: "y un estado"
  - lines: [3, 4]
    at: "Esos son sus atributos"
code: |-
  public class Tarea
  {
      public string Title { get; set; }
      public Status Status { get; set; }
  }
```

#### Enum: opciones conocidas

El estado no puede ser cualquier texto. Un enum define un conjunto de opciones conocidas. Estos son los tres estados que puede tener una tarea.

```scene
id: oop-enum
type: code
language: csharp
focus:
  - lines: [1]
    at: "Un enum define"
  - lines: [3, 4, 5]
    at: "Estos son los tres estados"
code: |-
  public enum Status
  {
      Pending,
      InProgress,
      Done
  }
```

#### El constructor

Un constructor es un código especial que prepara el objeto cuando lo creamos. Se llama igual que la clase, puede recibir datos y deja el objeto listo para usar. Aquí recibe el título y empieza la tarea como pendiente.

```scene
id: oop-constructor
type: code
language: csharp
focus:
  - lines: [6, 7, 8, 9, 10]
    at: "Un constructor es"
  - lines: [1, 6]
    at: "Se llama igual que la clase"
  - lines: [6]
    at: "puede recibir datos"
  - lines: [8]
    at: "Aquí recibe el título"
  - lines: [9]
    at: "empieza la tarea como pendiente"
code: |-
  public class Tarea
  {
      public string Title { get; set; }
      public Status Status { get; set; }

      public Tarea(string title)
      {
          Title = title;
          Status = Status.Pending;
      }
  }
```

#### Un método en un controlador

Un método es una acción que un objeto puede realizar. Este controlador sencillo tiene una lista de tareas y un método que las devuelve. Primero va public, luego lo que devuelve, después el nombre y los paréntesis. Dentro de las llaves está lo que hace.

```scene
id: oop-method
type: code
language: csharp
focus:
  - lines: [5]
    at: "Un método es"
  - lines: [3]
    at: "una lista de tareas"
  - lines: [5]
    at: "y un método que las devuelve"
  - lines: [6, 7, 8]
    at: "Dentro de las llaves"
code: |-
  public class TareasController
  {
      private List<Tarea> tareas = new();

      public List<Tarea> ObtenerTodas()
      {
          return tareas;
      }
  }
```

#### Usar los objetos desde afuera

Desde fuera de la clase, creamos un objeto con new, que llama al constructor. Después usamos sus propiedades y sus métodos con un punto. Todo esto funciona porque están marcados como public, es decir, que se pueden acceder desde cualquier parte de la aplicación. Si algo debe quedar oculto para el resto de la aplicación, lo marcamos como private, como la lista del controlador. Son temas de diseño que veremos más adelante.

```scene
id: oop-use
type: code
language: csharp
focus:
  - lines: [1]
    at: "creamos un objeto con new"
  - lines: [2]
    at: "Después usamos sus propiedades"
  - lines: [5]
    at: "y sus métodos"
  - lines: [1, 2, 4, 5]
    at: "Todo esto funciona porque están marcados como public"
  - lines: [7]
    at: "lo marcamos como private"
code: |-
  var tarea = new Tarea("Comprar café");
  tarea.Status = Status.InProgress;

  var controlador = new TareasController();
  var tareas = controlador.ObtenerTodas();

  // controlador.tareas no se puede usar desde aquí: es private
```

### 8. Así se ve en nuestro código C#

Nuestro backend está escrito en C#, un lenguaje orientado a objetos. Tenemos una clase que representa cada tarea y un enum con sus estados. También tenemos otros objetos, como el controlador, que llaman métodos para consultar y guardar datos. Así se construye el programa: distintos objetos que colaboran entre sí.

```scene
id: oop-real-project
type: code
language: csharp
code: |-
  // Tarea.cs
  public class Tarea
  {
      public string Title { get; set; } = "";
      public Status Status { get; set; }
  }

  // Status.cs
  public enum Status
  {
      Pending,
      InProgress,
      Done
  }

  // TareasController.cs
  return await _db.Tareas.ToListAsync();
highlights: [2, 9, 17]
source: repositorio
show: "Pantalla dividida: a la izquierda Tarea.cs y Status.cs (datos y estados); a la derecha una sola línea real de TareasController.cs (llamada entre objetos). Dibujar una flecha del controlador hacia _db.Tareas. No mostrar todavía el controlador entero."
files:
  - src/back/TareaApi/Models/Tarea.cs
  - src/back/TareaApi/Models/Status.cs
  - src/back/TareaApi/Controllers/TareasController.cs
highlight:
  - "public class Tarea"
  - "public enum Status"
  - "_db.Tareas.ToListAsync()"
```

```exercise
id: oop-check
type: multiple-choice
prompt: "En una clase, ¿qué diferencia hay entre una propiedad y un método?"
choices:
  - "La propiedad contiene un dato; el método realiza una acción"
  - "Ambos son nombres para una base de datos"
  - "El método contiene datos y la propiedad ejecuta acciones"
answer: 0
explanation: "Título es un dato de la tarea; consultar tareas es una acción."
```

### 9. Inyección de dependencias

El controlador necesita acceso a la base de datos. En lugar de encargarse de construir esa herramienta, la recibe ya preparada cuando se crea. Eso se llama inyección de dependencias. En nuestro caso, la aplicación prepara un TareaContext y se lo entrega al constructor del controlador. Después el controlador lo utiliza para trabajar con las tareas.

```scene
id: dependency-injection
type: code
language: csharp
source: repositorio
show: "Mostrar en dos bloques conectados: registro de TareaContext en Program.cs → parámetro del constructor de TareasController → campo _db. Resaltar la flecha de entrega. Código sin lectura de nombres de archivos."
files:
  - src/back/TareaApi/Program.cs
  - src/back/TareaApi/Controllers/TareasController.cs
code: |-
  // Program.cs
  builder.Services.AddDbContext<TareaContext>(
      options => options.UseSqlite(connectionString));

  // TareasController.cs
  public TareasController(TareaContext db)
  {
      _db = db;
  }
```

### 10. Entity Framework Core

Ahora necesitamos trabajar con la base de datos. Para eso usamos Entity Framework Core, o EF Core. Nos permite consultar, agregar y modificar tareas usando código C#, sin escribir directamente las instrucciones SQL. SQL es el lenguaje de las bases de datos y lo aprenderemos en otras lecciones. Por ahora, EF Core hace ese trabajo por nosotros.

```scene
id: ef-intro
type: visual
visual: backend
plain: true
steps:
  - "C#: objetos Tarea"
  - "EF Core: traduce operaciones y administra los cambios"
  - "SQLite: guarda las tareas en una tabla"
items:
  - icon: 📋
    label: Objeto Tarea
  - icon: 🔄
    label: EF Core
  - icon: 💾
    label: Base de datos
```

### 11. Consultas y comandos

Una consulta lee datos sin modificarlos. Podemos pedir todas las tareas o buscar una por su número. En cambio, cuando agregamos, actualizamos o borramos una tarea, estamos cambiando datos. En EF Core usamos métodos de C# para esas operaciones, y guardamos los cambios para que permanezcan en la base de datos.

```scene
id: ef-operations
type: code
language: csharp
source: repositorio
show: "Dos columnas. Izquierda: CONSULTAR → ToListAsync / FindAsync → aparecen tareas en una lista. Derecha: MODIFICAR → Add / Remove / cambio de propiedades → SaveChangesAsync → cambia la tabla. Los fragmentos corresponden a los métodos reales del controlador."
file: src/back/TareaApi/Controllers/TareasController.cs
code: |-
  // Consultar
  await _db.Tareas.ToListAsync();
  await _db.Tareas.FindAsync(id);

  // Crear y guardar
  _db.Tareas.Add(tarea);
  await _db.SaveChangesAsync();
```

```exercise
id: ef-check
type: multiple-choice
prompt: "Después de agregar una tarea con EF Core, ¿qué nos permite guardar el cambio en la base de datos?"
choices:
  - "SaveChangesAsync()"
  - "ToListAsync()"
  - "FindAsync()"
answer: 0
explanation: "SaveChangesAsync() confirma los cambios pendientes."
```

### 12. Migraciones: cambiar la base de datos

¿Y si mañana queremos guardar una fecha de vencimiento para cada tarea? No basta con agregar ese dato al código: también necesitamos modificar la estructura de la base de datos. Para eso sirven las migraciones. Nuestro ejemplo ya tiene una que crea las tareas y otra que agrega la fecha, conservando los datos anteriores.

```scene
id: ef-migrations
type: visual
visual: timeline
plain: true
items:
  - icon: 📋
    label: InitialCreate
    detail: "Crea Id, Title, Description y Status"
  - icon: 📅
    label: AddDueDate
    detail: "Agrega DueDate a la tabla existente"
  - icon: ✅
    label: Resultado
    detail: "La tabla evoluciona sin borrar las tareas"
```

### 13. El controlador: la puerta de entrada

Ya tenemos las piezas. El controlador es la puerta de entrada de nuestra API: recibe una petición HTTP, elige qué operación ejecutar y devuelve una respuesta. Como ya recibió el acceso a la base de datos mediante su constructor, puede consultar o modificar tareas sin encargarse de preparar la conexión.

```scene
id: controller-entry
type: code
language: csharp
code: |-
  [Route("api/tareas")]
  public class TareasController : ControllerBase
  {
      public TareasController(TareaContext db)
      {
          _db = db;
      }

      [HttpGet]
      // ...
      [HttpPost]
      // ...
      [HttpPut("{id}")]
      // ...
      [HttpDelete("{id}")]
      // ...
  }
highlights: [1, 9, 11, 13, 15]
source: repositorio
show: "Mostrar la cabecera real de TareasController.cs y destacar por separado [Route], el constructor con _db, y los atributos [HttpGet], [HttpPost], [HttpPut], [HttpDelete]. Señalar que cada atributo conecta una petición HTTP con un método. No mostrar todavía las implementaciones completas."
file: src/back/TareaApi/Controllers/TareasController.cs
highlight:
  - '[Route("api/tareas")]'
  - "TareasController(TareaContext db)"
  - "[HttpGet]"
  - "[HttpPost]"
  - '[HttpPut("{id}")]'
  - '[HttpDelete("{id}")]'
```

### 14. Consultar tareas: de Swagger a la respuesta

Miremos una operación completa. Desde Swagger pedimos la lista de tareas. El controlador recibe esa petición, consulta la base de datos mediante EF Core y devuelve las tareas. Swagger nos muestra el resultado, como lo recibiría cualquier programa que utilice esta API.

```scene
id: swagger-get
type: visual
visual: swagger-mock
stage: request-response
header: "GET /api/tareas"
show: "Simular clic en GET → Try it out → Execute. Animar el viaje de petición hacia el método GetAll(), luego _db.Tareas.ToListAsync(), y volver a Swagger con 200 OK y una respuesta JSON de ejemplo. El JSON se ve en pantalla, no se lee en voz alta."
request:
  method: GET
  path: /api/tareas
response:
  status: 200
  json: |-
    [
      { "id": 1, "title": "Comprar café", "description": "", "status": "Pending", "dueDate": null }
    ]
```

### 15. Crear tareas: enviar datos

Ahora hagamos lo contrario: enviar información al backend. En Swagger escribimos el título, la descripción y el estado de una tarea nueva. Cuando ejecutamos POST, el controlador recibe esos datos, crea la tarea en la base de datos y devuelve la información de la tarea creada, incluido su identificador.

```scene
id: swagger-post
type: visual
visual: swagger-mock
stage: request-response
header: "POST /api/tareas"
show: "Simular abrir POST → Try it out → escribir el JSON → Execute. Mostrar el cuerpo entrando al controlador, Add() y SaveChangesAsync() en secuencia; respuesta 201 Created con id generado. No introducir frontend."
request:
  method: POST
  path: /api/tareas
  json: |-
    { "title": "Comprar café", "description": "Para mañana", "status": "Pending" }
response:
  status: 201
  json: |-
    { "id": 1, "title": "Comprar café", "description": "Para mañana", "status": "Pending", "dueDate": null }
```

### 16. Cambiar el estado de una tarea

La tarea ya existe, pero ahora estamos trabajando en ella. Podemos enviar una petición PUT con el mismo identificador y cambiar su estado a en progreso. El controlador busca la tarea, modifica sus datos y guarda el cambio. Si volvemos a consultarla, veremos el nuevo estado.

```scene
id: swagger-put
type: visual
visual: swagger-mock
stage: request-response
header: "PUT /api/tareas/1"
show: "Simular seleccionar PUT, escribir id 1 y enviar el JSON. Mostrar la tarjeta de la tarea cambiando visualmente de Pending a InProgress. Swagger devuelve 204 No Content; después ejecutar GET /api/tareas/1 para verificar el nuevo estado."
request:
  method: PUT
  path: /api/tareas/1
  json: |-
    { "title": "Comprar café", "description": "Para mañana", "status": "InProgress" }
response:
  status: 204
followup:
  method: GET
  path: /api/tareas/1
  status: 200
  json: |-
    { "id": 1, "title": "Comprar café", "description": "Para mañana", "status": "InProgress", "dueDate": null }
```

### 17. Te toca: probar Swagger y modificar el código

Ahora vas a probar tú mismo las operaciones. Inicia la aplicación, abre Swagger y crea una tarea. Consúltala, cambia su estado y comprueba que quedó guardado. Después vamos a hacer dos cambios pequeños en el código: ordenar las tareas por título y agregar un nuevo estado. Puedes pedirle ayuda al agente, pero revisa qué cambió y verifica el resultado.

```scene
id: practice-swagger
type: visual
visual: swagger-mock
stage: hands-on
header: "http://localhost:5080/swagger"
show: "Mostrar navegador real o simulado con Swagger, en orden: POST crear → GET listar → PUT cambiar estado → GET verificar. En una esquina, indicar ./run/build.sh y ./run/start.sh solo como apoyo visual. Cerrar con VS Code abierto en GetAll() y Status.cs."
steps:
  - "Crear una tarea con POST"
  - "Consultar con GET"
  - "Cambiar su estado con PUT"
  - "Consultar de nuevo y comprobar el cambio"
```

```exercise
id: practice-api
type: checkpoint
prompt: "Creé una tarea, cambié su estado y confirmé el resultado desde Swagger."
explanation: "La API queda comprobada cuando las peticiones devuelven los datos y estados esperados."
```

```exercise
id: practice-sort
type: checkpoint
prompt: "Ordené las tareas alfabéticamente modificando GetAll() y comprobé el orden en Swagger."
explanation: "Pista: puedes usar OrderBy(t => t.Title) antes de ToListAsync(). Prueba creando dos tareas en orden inverso al alfabético."
```

```exercise
id: practice-enum
type: checkpoint
prompt: "Agregué el estado Cancelled al enum Status y comprobé que puedo usarlo al actualizar una tarea."
explanation: "Busca los estados existentes en Status.cs; luego prueba desde Swagger con el nuevo valor."
```
