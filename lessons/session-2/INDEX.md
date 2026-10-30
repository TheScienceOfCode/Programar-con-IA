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
    detail: Pide o muestra los datos
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

¿Cómo se comunican estos programas por la web? Usan HTTP, un conjunto de reglas para enviar peticiones y recibir respuestas. Por ejemplo, pedimos nuestras tareas; el servidor las busca y nos devuelve una respuesta con los datos. Si algo falla, también nos lo indica.

```scene
id: http-request-response
type: visual
visual: backend
plain: true
steps:
  - "Cliente → servidor: quiero ver mis tareas"
  - "Servidor: consulta los datos"
  - "Servidor → cliente: estas son tus tareas"
items:
  - icon: 📤
    label: Petición HTTP
  - icon: 📥
    label: Respuesta HTTP
    detail: "Datos + resultado (por ejemplo, 200 OK)"
```

### 4. REST y RESTful

REST es una manera de organizar las API que utilizan HTTP. En lugar de inventar una operación diferente para cada cosa, trabajamos con recursos. En nuestro ejemplo, el recurso es una tarea. Cuando una API sigue estas convenciones, solemos llamarla RESTful.

```scene
id: rest-concept
type: visual
visual: backend
plain: true
steps:
  - "Recurso: tareas"
  - "Una misma dirección identifica el conjunto"
  - "El método HTTP indica lo que queremos hacer"
items:
  - icon: 📋
    label: Tareas
    detail: El recurso
  - icon: 🔄
    label: Operaciones
    detail: Consultar, crear, actualizar, borrar
```

### 5. Métodos HTTP en nuestra API

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

### 6. Programación orientada a objetos

Para entender el código necesitamos un concepto importante: la programación orientada a objetos. Es una forma de organizar el programa en clases que reúnen datos y comportamientos. Los datos, llamados atributos o propiedades, son por ejemplo el título y el estado de una tarea; los métodos son las acciones que puede realizar. Un constructor prepara el objeto cuando lo creamos, y un enum permite definir opciones conocidas, como los estados de una tarea.

```scene
id: oop-basics
type: code
language: csharp
source: ejemplo-didactico
show: "Ejemplo inventado SOLO para explicar los conceptos. Resaltar en secuencia clase, propiedad, constructor, método y enum. Mostrar al lado una tarjeta de tarea que cambia a Terminada al invocar Completar()."
code: |-
  enum Estado { Pendiente, EnProgreso, Terminada }

  class TareaEjemplo
  {
      public string Titulo { get; set; }
      public Estado Estado { get; private set; }
      = Estado.Pendiente;

      public TareaEjemplo(string titulo) { Titulo = titulo; }
      public void Completar() { Estado = Estado.Terminada; }
  }
```

### 7. Así se ve en nuestro código C#

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

### 8. Inyección de dependencias

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

### 9. Entity Framework Core

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

### 10. Consultas y comandos

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

### 11. Migraciones: cambiar la base de datos

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

### 12. El controlador: la puerta de entrada

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

### 13. Consultar tareas: de Swagger a la respuesta

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

### 14. Crear tareas: enviar datos

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

### 15. Cambiar el estado de una tarea

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

### 16. Te toca: probar Swagger y modificar el código

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
