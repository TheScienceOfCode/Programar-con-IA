---
title: "Lección 2: Entiende el backend de una API"
courseTitle: "Aprende a\nProgramar con IA"
language: es
objectives:
  - Entender qué son una API, HTTP y REST
  - Reconocer clases, propiedades, enums, constructores y métodos en C#
  - Comprender inyección de dependencias, EF Core y migraciones
  - Leer, modificar y probar un controlador real
prerequisites:
  - Lección 1
  - VS Code con un agente de programación y Docker disponible
---
# Lección 2 — Entiende el backend de una API

**Proyecto:** Aprende a Programar con IA  
**Ejemplo:** https://github.com/TheScienceOfCode/Ejemplos-IA/tree/Todo-IA  
**Formato:** video guiado, una pantalla por parte, con pregunta y botón Continuar.  
**Público:** principiantes que ya construyeron su primera aplicación con IA.  
**Objetivo práctico:** entender el código lo suficiente para comenzar a editarlo.

**Para producir el tutorial:** cada `###` es una pantalla. La narración es el texto del apartado; `scene` indica lo que se muestra; `exercise` contiene preguntas o prácticas. Al mostrar código, usar los archivos reales de la rama `Todo-IA`, resaltando únicamente las líneas necesarias. Los bloques `visual: code` describen una vista de código; si Autotorial todavía no la admite, implementarla o adaptarla sin perder el código ni su resaltado. No modificar el ejemplo solo para grabar las explicaciones.

## Partes

### 1. El proyecto que vamos a entender

La vez pasada le pedimos a una IA que construyera una aplicación. Hoy vamos a mirar por dentro un backend de verdad: una API para crear, consultar, actualizar y borrar tareas. No tiene interfaz gráfica todavía. Todo lo probaremos desde el navegador con Swagger.

En el repositorio, `src/back` contiene el backend, `run` los scripts para ejecutarlo y `src/front` está reservado para después. Puedes pedirle a tu agente que descargue la rama `Todo-IA`, ejecute `./run/build.sh` y `./run/start.sh`, y abra `http://localhost:5080/swagger`.

```scene
id: project-overview
type: visual
visual: timeline
items:
  - icon: 📁
    label: src/back/TodoApi
    detail: Código C# del backend
  - icon: 🛠️
    label: run/
    detail: Construir, iniciar, detener y probar
  - icon: 🌐
    label: Swagger
    detail: localhost:5080/swagger
  - icon: 🧪
    label: run/test.sh
    detail: Pruebas HTTP de la API
```
```exercise
id: check-project
type: checkpoint
prompt: Ya tengo abierto el ejemplo y puedo ver sus endpoints en Swagger
explanation: Perfecto. Empecemos por entender qué estamos viendo.
```

### 2. ¿Qué es una API?

Una API es una forma definida de comunicarse con un programa. En nuestro ejemplo, otro programa puede pedirle al backend la lista de tareas o decirle que guarde una nueva. No necesita saber cómo funciona la base de datos: solo conocer las operaciones que ofrece la API.

Cuando consultamos `/api/todos`, el servidor nos responde con datos, normalmente en formato JSON. JSON es texto estructurado que representa información, por ejemplo una tarea con su título y estado.

```scene
id: api-intro
type: visual
visual: backend
steps:
  - 'Cliente: dame las tareas'
  - 'API: GET /api/todos'
  - 'Servidor: consulta los datos'
  - 'Respuesta JSON: [{"id":1,"title":"Estudiar","status":"Pending"}]'
```
```exercise
id: quiz-api
type: multiple-choice
prompt: ¿Para qué sirve una API en este ejemplo?
choices:
  - Para definir cómo otros programas consultan o modifican nuestras tareas
  - Para dibujar botones en la pantalla
  - Para reemplazar la base de datos
answer: 0
explanation: La API expone operaciones; otros programas pueden utilizarlas sin conocer su funcionamiento interno.
```

### 3. HTTP: peticiones y respuestas

HTTP es el protocolo que usa el cliente para hablar con nuestro servidor. Una petición contiene una dirección y un método, como `GET` o `POST`. También puede enviar datos en un cuerpo JSON. El servidor responde con un código de estado y, cuando hace falta, con datos.

Por ejemplo, `GET /api/todos/1` pide la tarea número 1. Si existe, recibimos `200 OK` y la tarea. Si no existe, recibimos `404 Not Found`.

```scene
id: http-request
type: visual
visual: timeline
items:
  - icon: 📤
    label: Petición
    detail: GET /api/todos/1
  - icon: ⚙️
    label: Backend
    detail: Busca la tarea 1
  - icon: ✅
    label: Respuesta encontrada
    detail: 200 OK + JSON
  - icon: ❓
    label: Respuesta no encontrada
    detail: 404 Not Found
```
```exercise
id: quiz-http
type: multiple-choice
prompt: ¿Qué significa un 404 en GET /api/todos/99999?
choices:
  - Que la tarea solicitada no se encontró
  - Que la tarea se guardó correctamente
  - Que el servidor devolvió todas las tareas
answer: 0
explanation: 404 significa que el recurso solicitado no se encontró.
```

### 4. REST: las operaciones sobre tareas

REST es una forma de organizar APIs HTTP alrededor de recursos. Nuestro recurso es una tarea, o *ToDo*. La ruta identifica el recurso y el método expresa qué queremos hacer. Estas son las cinco operaciones reales del proyecto:

```scene
id: rest-routes
type: visual
visual: timeline
items:
  - icon: 📋
    label: GET /api/todos
    detail: Listar tareas · 200
  - icon: 🔎
    label: GET /api/todos/{id}
    detail: Consultar una tarea · 200 o 404
  - icon: ➕
    label: POST /api/todos
    detail: Crear una tarea · 201
  - icon: ✏️
    label: PUT /api/todos/{id}
    detail: Actualizar una tarea · 204 o 404
  - icon: 🗑️
    label: DELETE /api/todos/{id}
    detail: Borrar una tarea · 204 o 404
```
```exercise
id: quiz-rest
type: multiple-choice
prompt: Si queremos cambiar el título de la tarea 3, ¿qué usamos?
choices:
  - GET /api/todos
  - PUT /api/todos/3
  - DELETE /api/todos/3
answer: 1
explanation: PUT actualiza el recurso que identifica la ruta. El cuerpo JSON envía los nuevos valores.
```

### 5. Programación orientada a objetos: clases y objetos

En C# organizamos buena parte del código usando clases. Una clase define cómo es algo y qué puede hacer. Un objeto es una instancia concreta de esa clase.

Abre `Models/Todo.cs`. La clase `Todo` describe nuestras tareas. Por ejemplo, podemos crear un objeto con título «Estudiar C#». La clase es el modelo; ese objeto es una tarea específica.

```scene
id: oop-class
type: code
language: csharp
file: src/back/TodoApi/Models/Todo.cs
code: |-
  public class Todo
  {
      public int Id { get; set; }
      public string Title { get; set; } = "";
      public string Description { get; set; } = "";
      public Status Status { get; set; }
      public DateTime? DueDate { get; set; }
  }
```
```exercise
id: quiz-class
type: multiple-choice
prompt: ¿Cuál es la diferencia entre clase y objeto?
choices:
  - La clase describe la estructura; el objeto es una instancia concreta
  - La clase guarda datos y el objeto solo dibuja pantallas
  - Son exactamente lo mismo
answer: 0
explanation: Todo es la clase; cada tarea concreta que creamos es un objeto Todo.
```

### 6. Propiedades y tipos: los datos de una tarea

A los datos de un objeto solemos llamarlos atributos. En este código de C# están declarados como **propiedades**, con `get` para leer y `set` para cambiar su valor. `Id` es un número entero; `Title` y `Description` son textos; `Status` tendrá uno de varios estados; `DueDate` es una fecha opcional. El signo `?` significa que puede no tener valor.

```scene
id: todo-properties
type: code
language: csharp
file: src/back/TodoApi/Models/Todo.cs
code: |-
  public int Id { get; set; }                   // Número entero
  public string Title { get; set; } = "";       // Texto
  public string Description { get; set; } = ""; // Texto
  public Status Status { get; set; }            // Estado
  public DateTime? DueDate { get; set; }        // Fecha opcional
```
```exercise
id: quiz-properties
type: multiple-choice
prompt: ¿Qué propiedad guardarías para saber cuándo vence una tarea?
choices:
  - DueDate
  - Title
  - Id
answer: 0
explanation: DueDate representa una fecha opcional.
```

### 7. Enums: una lista de valores permitidos

Abre `Models/Status.cs`. Un `enum` define un conjunto de opciones con nombre. Así evitamos escribir estados arbitrarios o equivocarnos al escribirlos. Aquí una tarea puede estar `Pending`, `InProgress` o `Done`. En una petición JSON enviamos el estado como texto, porque `Program.cs` configura esa conversión.

```scene
id: status-enum
type: code
language: csharp
file: src/back/TodoApi/Models/Status.cs
code: |-
  public enum Status
  {
      Pending,
      InProgress,
      Done
  }
```
```exercise
id: quiz-enum
type: multiple-choice
prompt: ¿Para qué usar un enum en lugar de un texto libre?
choices:
  - Para definir un conjunto conocido de opciones
  - Para almacenar imágenes
  - Para crear rutas HTTP
answer: 0
explanation: Un enum deja claros los valores que acepta el programa.
```

### 8. Constructores y métodos

Un constructor prepara un objeto cuando se crea. Puede recibir datos necesarios para funcionar. En `TodoContext.cs` hay uno: recibe opciones de configuración y las pasa a `DbContext`. La clase `Todo` no declara constructor propio, así que C# le proporciona uno sin parámetros.

Un método, en cambio, es una acción que un objeto puede ejecutar. En `TodosController.cs`, `GetAll()` es un método que obtiene tareas. Los paréntesis ayudan a reconocer los métodos; las propiedades se usan como datos.

```scene
id: constructors-methods
type: code
language: csharp
file: src/back/TodoApi/TodoContext.cs
code: |-
  public class TodoContext : DbContext
  {
      public TodoContext(DbContextOptions<TodoContext> options)
          : base(options) { }

      public DbSet<Todo> Todos => Set<Todo>();
  }
```
```exercise
id: quiz-method
type: multiple-choice
prompt: En el controlador, ¿cuál es un método?
choices:
  - GetAll()
  - Title
  - Description
answer: 0
explanation: GetAll() ejecuta una acción; Title y Description son propiedades.
```

### 9. Inyección de dependencias: recibir lo que necesitamos

Un controlador necesita acceso a los datos. Podría construir esa conexión por su cuenta, pero ASP.NET Core puede entregársela. Eso es **inyección de dependencias**: la clase declara qué necesita en su constructor y el sistema se lo proporciona.

En `Program.cs`, `AddDbContext<TodoContext>` registra el contexto y configura SQLite. En `TodosController.cs`, el constructor recibe un `TodoContext` y lo guarda en `_db`. Así el controlador puede usarlo sin crearlo manualmente.

```scene
id: dependency-injection
type: code
language: csharp
file: src/back/TodoApi/Program.cs + Controllers/TodosController.cs
code: |-
  // Program.cs: registro
  builder.Services.AddDbContext<TodoContext>(
      options => options.UseSqlite(connectionString));

  // TodosController.cs: recepción
  private readonly TodoContext _db;
  public TodosController(TodoContext db)
  {
      _db = db;
  }
```
```exercise
id: quiz-di
type: multiple-choice
prompt: ¿Quién entrega TodoContext al constructor del controlador?
choices:
  - El sistema de inyección de dependencias de ASP.NET Core
  - El navegador
  - Swagger
answer: 0
explanation: El contexto se registra en Program.cs y ASP.NET Core lo proporciona al crear el controlador.
```

### 10. EF Core: clases que representan datos

**Entity Framework Core**, o EF Core, nos permite trabajar con datos desde C# sin escribir SQL para cada operación. `TodoContext` representa el acceso a la base de datos, y `DbSet<Todo> Todos` representa el conjunto de tareas que podemos consultar o modificar.

El proyecto utiliza SQLite. La base guarda una tabla `Todos` con las columnas correspondientes a las propiedades de `Todo`. No confundas `TodoContext` con una tarea: el primero sirve para acceder a los datos; `Todo` describe cada tarea.

```scene
id: ef-context
type: visual
visual: backend
steps:
  - TodoController recibe TodoContext
  - TodoContext expone DbSet<Todo> Todos
  - EF Core genera las operaciones de datos
  - SQLite conserva los registros de la tabla Todos
```
```exercise
id: quiz-ef
type: multiple-choice
prompt: En este proyecto, ¿qué representa _db.Todos?
choices:
  - El conjunto de tareas accesibles mediante EF Core
  - El nombre del navegador
  - El estado de una sola tarea
answer: 0
explanation: Es un DbSet<Todo>, utilizado para consultar y cambiar tareas en la base de datos.
```

### 11. Consultas: leer tareas con EF Core

Una consulta obtiene información sin modificarla. En el controlador, `ToListAsync()` obtiene todas las tareas y `FindAsync(id)` busca una por su identificador. Podemos filtrar con `Where` u ordenar con `OrderBy`.

Verás `async` y `await`: permiten esperar operaciones como una consulta a la base de datos sin bloquear innecesariamente el servidor. Por ahora basta con reconocerlos.

```scene
id: ef-queries
type: code
language: csharp
file: src/back/TodoApi/Controllers/TodosController.cs
code: |-
  // Todas las tareas
  return await _db.Todos.ToListAsync();

  // Una tarea por ID
  var todo = await _db.Todos.FindAsync(id);

  // Ejemplo adicional: solo tareas pendientes
  var pending = await _db.Todos
      .Where(t => t.Status == Status.Pending)
      .ToListAsync();
```
```exercise
id: quiz-queries
type: multiple-choice
prompt: Si quiero obtener solo tareas pendientes, ¿qué operación me ayuda a filtrarlas?
choices:
  - Where(...)
  - Remove(...)
  - SaveChangesAsync()
answer: 0
explanation: Where filtra los elementos según una condición.
```

### 12. Comandos: guardar, actualizar y borrar

Consultar no es lo mismo que cambiar datos. Para crear, el controlador llama a `Add(todo)` y después a `SaveChangesAsync()`. Para actualizar, busca la tarea, cambia sus propiedades y guarda los cambios. Para borrar, llama a `Remove(todo)` y vuelve a guardar.

`SaveChangesAsync()` es importante: agregar, modificar o quitar un objeto en el contexto no equivale todavía a confirmar el cambio en la base de datos.

```scene
id: ef-commands
type: code
language: csharp
file: src/back/TodoApi/Controllers/TodosController.cs
code: |-
  // Crear
  _db.Todos.Add(todo);
  await _db.SaveChangesAsync();

  // Actualizar una tarea ya consultada
  existing.Title = todo.Title;
  await _db.SaveChangesAsync();

  // Borrar
  _db.Todos.Remove(todo);
  await _db.SaveChangesAsync();
```
```exercise
id: quiz-save
type: multiple-choice
prompt: Después de cambiar Title en una tarea consultada, ¿qué falta para guardar el cambio?
choices:
  - Llamar a SaveChangesAsync()
  - Llamar a ToListAsync()
  - Recargar Swagger sin hacer nada más
answer: 0
explanation: SaveChangesAsync confirma las modificaciones pendientes en la base de datos.
```

### 13. Migraciones: cuando cambia la estructura de los datos

Imagina que nuestra primera versión de `Todo` no tenía fecha de vencimiento. Después agregamos `DueDate`. Hay que actualizar la tabla para que esa columna exista. Para eso sirven las **migraciones**: registran cambios en la estructura de la base de datos.

Este ejemplo contiene `InitialCreate`, que crea `Todos`, y `AddDueDate`, que agrega la fecha opcional. En `Program.cs`, `Database.Migrate()` aplica las migraciones pendientes cuando arranca la API. Las tareas se conservan en el volumen Docker `todo-data` incluso si detenemos la aplicación.

```scene
id: ef-migrations
type: visual
visual: timeline
items:
  - icon: 🏗️
    label: InitialCreate
    detail: Crea la tabla Todos
  - icon: 📅
    label: AddDueDate
    detail: Agrega la columna opcional DueDate
  - icon: ▶️
    label: Database.Migrate()
    detail: Aplica cambios pendientes al iniciar
  - icon: 💾
    label: Volumen Docker todo-data
    detail: Conserva las tareas al detener y reiniciar
```
```exercise
id: quiz-migrations
type: multiple-choice
prompt: Si agregamos una propiedad nueva que debe guardarse en la base de datos, ¿qué necesitamos normalmente?
choices:
  - Crear y aplicar una migración
  - Cambiar solamente los colores de Swagger
  - Borrar todas las tareas existentes
answer: 0
explanation: La migración lleva el esquema de la base de datos a la nueva versión sin tener que recrearlo todo.
```

### 14. El controlador: conectar HTTP con EF Core

Ahora podemos leer el controlador completo. `[Route("api/todos")]` indica la dirección principal; `[HttpGet]` marca el método que atiende una petición GET. Esos corchetes son **atributos de C#**: indicaciones para ASP.NET Core, no propiedades de la tarea.

El constructor recibe `_db` por inyección de dependencias. `GetAll()` consulta la base de datos. `Get(id)` busca una tarea y responde `NotFound()` si no existe. Aquí se conectan todas las piezas que acabamos de estudiar.

```scene
id: controller-get
type: code
language: csharp
file: src/back/TodoApi/Controllers/TodosController.cs
code: |-
  [ApiController]
  [Route("api/todos")]
  public class TodosController : ControllerBase
  {
      private readonly TodoContext _db;
      public TodosController(TodoContext db) { _db = db; }

      [HttpGet]
      public async Task<ActionResult<List<Todo>>> GetAll()
      {
          return await _db.Todos.ToListAsync();
      }

      [HttpGet("{id}")]
      public async Task<ActionResult<Todo>> Get(int id)
      {
          var todo = await _db.Todos.FindAsync(id);
          if (todo == null) return NotFound();
          return todo;
      }
  }
```
```exercise
id: quiz-controller
type: multiple-choice
prompt: ¿Qué línea obtiene los datos que devuelve GET /api/todos?
choices:
  - _db.Todos.ToListAsync()
  - [Route("api/todos")]
  - private readonly TodoContext _db;
answer: 0
explanation: La ruta y el constructor preparan el controlador, pero ToListAsync ejecuta la consulta.
```

### 15. Sigue una tarea de principio a fin

Probemos el recorrido completo. Desde Swagger enviamos un `POST /api/todos` con título, descripción y estado. El controlador recibe un objeto `Todo`, lo agrega al contexto, guarda los cambios y responde `201 Created`. Después usamos `GET` para encontrarlo, `PUT` para cambiarlo y `DELETE` para borrarlo. Las respuestas `204 No Content` de PUT y DELETE indican éxito sin cuerpo de respuesta.

```scene
id: crud-walkthrough
type: visual
visual: timeline
items:
  - icon: ➕
    label: POST /api/todos
    detail: '{"title":"Estudiar C#","description":"Leer el código","status":"Pending"}'
  - icon: 🔎
    label: GET /api/todos/{id}
    detail: Comprueba la tarea creada
  - icon: ✏️
    label: PUT /api/todos/{id}
    detail: Cambia title o status
  - icon: 🗑️
    label: DELETE /api/todos/{id}
    detail: Elimina la tarea
  - icon: 🧪
    label: ./run/test.sh
    detail: Comprueba automáticamente las operaciones principales
```
```exercise
id: check-crud
type: checkpoint
prompt: Ya creé, consulté, actualicé y borré una tarea desde Swagger
explanation: Ahora conoces el recorrido completo, desde HTTP hasta SQLite.
```

### 16. Práctica: modifica tú el código

Vamos a hacer tres cambios pequeños. Hazlos en VS Code; puedes pedirle al agente que te explique una línea, pero intenta escribir el cambio tú. Después de cada cambio, reconstruye el contenedor con `./run/build.sh`, reinicia con `./run/restart.sh` y comprueba el resultado en Swagger. Al final ejecuta `./run/test.sh`.

#### Ejercicio 1. Ordena las tareas

En `GetAll()`, cambia la consulta para devolver las tareas ordenadas alfabéticamente por título. Pista: usa `OrderBy(t => t.Title)` antes de `ToListAsync()`. Crea dos tareas con títulos distintos y comprueba el orden.

```scene
id: practice-sort
type: code
language: csharp
file: src/back/TodoApi/Controllers/TodosController.cs
code: |-
  // Antes
  return await _db.Todos.ToListAsync();

  // Tu objetivo: agregar OrderBy(t => t.Title)
  // antes de ToListAsync()
```

#### Ejercicio 2. Crea una nueva consulta

Agrega al controlador un endpoint `GET /api/todos/count` que devuelva el número de tareas. Usa `[HttpGet("count")]` y `_db.Todos.CountAsync()`. Crea y borra tareas desde Swagger para comprobar que el número cambia.

```scene
id: practice-count
type: code
language: csharp
file: src/back/TodoApi/Controllers/TodosController.cs
code: |-
  [HttpGet("count")]
  public async Task<int> GetCount()
  {
      return await _db.Todos.CountAsync();
  }
```

#### Ejercicio 3. Agrega otro estado

En `Status.cs`, agrega `Cancelled`. Reconstruye y prueba crear una tarea con `"status": "Cancelled"`. Comprueba que vuelve a aparecer al consultarla. En este proyecto el estado se guarda como número entero en SQLite y se representa como texto en JSON, así que agregar este valor no requiere cambiar la estructura de la tabla.

```scene
id: practice-enum
type: code
language: csharp
file: src/back/TodoApi/Models/Status.cs
code: |-
  public enum Status
  {
      Pending,
      InProgress,
      Done,
      Cancelled
  }
```
```exercise
id: check-practices
type: checkpoint
prompt: Comprobé mis tres cambios en Swagger y las pruebas existentes siguen pasando
explanation: Ya modificaste una consulta, agregaste un endpoint y ampliaste un enum.
```

### 17. Reto opcional: tu primera migración

Si quieres ir un poco más allá, agrega a `Todo` la propiedad `public bool IsImportant { get; set; }`. Pídele al agente que genere una migración de EF Core, pero que primero te muestre qué va a cambiar y te explique el archivo. Luego reconstruye, inicia y comprueba que puedes crear y consultar tareas con ese campo. Reinicia y verifica que se conserva.

```scene
id: challenge-migration
type: visual
visual: timeline
items:
  - icon: ✏️
    label: Edita Todo.cs
    detail: Agrega IsImportant de tipo bool
  - icon: 🤖
    label: Genera una migración
    detail: Pide ayuda al agente y revisa lo que cambió
  - icon: ▶️
    label: Reinicia la API
    detail: Database.Migrate() aplica la nueva migración
  - icon: ✅
    label: Verifica en Swagger
    detail: Guarda y vuelve a leer IsImportant
```
```exercise
id: check-migration-challenge
type: checkpoint
prompt: Terminé el reto o decidí continuar sin hacerlo
explanation: Ya tienes las bases para leer el backend y empezar a cambiarlo sin trabajar a ciegas.
```

### 18. Qué aprendimos

Una API ofrece operaciones para comunicarse con un programa. HTTP transporta las peticiones y REST ayuda a organizarlas. Las clases y sus propiedades representan datos; los métodos ejecutan acciones. La inyección de dependencias entrega al controlador lo que necesita. EF Core consulta y guarda en SQLite, y las migraciones actualizan la estructura de los datos.

Lo más importante: ya puedes abrir un archivo, reconocer qué hace, cambiar unas líneas y verificar tu resultado. Así se empieza a dominar el código que construimos con IA.

```scene
id: lesson-summary
type: visual
visual: timeline
items:
  - icon: 🌐
    label: HTTP y REST
    detail: Cómo se piden las operaciones
  - icon: 🧱
    label: Clases y métodos
    detail: Cómo se organiza el programa
  - icon: 🔌
    label: Inyección de dependencias
    detail: Cómo recibe el controlador el contexto
  - icon: 💾
    label: EF Core y migraciones
    detail: Cómo se leen y conservan los datos
  - icon: ✅
    label: Tu primer cambio
    detail: Leer, editar, ejecutar y comprobar
```
```exercise
id: check-finished
type: checkpoint
prompt: Terminé la lección 2
explanation: Ya puedes comenzar a explorar el backend por tu cuenta.
```
