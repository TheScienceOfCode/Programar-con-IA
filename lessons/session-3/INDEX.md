---
title: "Lección 3: Backend en ASP Core"
courseTitle: "Aprende a\nProgramar con IA"
language: es
objectives:
  - Entender qué ofrecen una API, HTTP y REST
  - Comprender cómo el controlador usa EF Core para consultar y guardar tareas
  - Probar la API desde Swagger y modificar código pequeño
prerequisites:
  - Lección 2
  - Docker y un editor de código
---

# Lección 3 — Backend en ASP Core

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
    detail: Estado.Pendiente
    steps:
      - Comprar café
      - Revisar el correo
  - icon: 🛠️
    label: En progreso
    detail: Estado.EnProgreso
    steps:
      - Preparar la clase
  - icon: ✅
    label: Terminado
    detail: Estado.Terminada
    steps:
      - Enviar la factura
```

### 3. HTTP: peticiones y respuestas

#### La dirección

Cuando abrimos el navegador y vamos a una dirección, esa dirección suele tener una estructura. Empieza con http, que indica el protocolo de comunicación. Es algo muy técnico, pero es lo que permite que programas diferentes puedan comunicarse por internet. Después viene el servidor: el lugar donde está la aplicación con la que estamos hablando. Aquí es nuestro propio computador, junto con el puerto por el que escucha. Y al final, el recurso que queremos pedir: en este caso, las tareas.

```scene
id: url-anatomy
type: visual
visual: url-anatomy
steps:
  - "Reglas que permiten que programas diferentes se comuniquen por internet"
  - "Dónde está la aplicación: nuestro computador y su puerto"
  - "Qué queremos pedir: las tareas"
items:
  - icon: 🤝
    label: "http://"
    detail: Protocolo
    at: "Empieza con http"
  - icon: 🖥️
    label: "localhost:5080"
    detail: Servidor
    at: "Después viene el servidor"
  - icon: 📋
    label: "/api/tareas"
    detail: Recurso
    at: "Y al final, el recurso"
```

#### Petición y respuesta

Cuando el frontend necesita obtener información, envía una petición http al backend, que llega hasta la base de datos. El backend devuelve una respuesta a esa petición, y el frontend la procesa. Dentro del backend, quien atiende cada petición es un controlador. El backend se divide en controladores, que son grupos de funciones, usualmente organizados por entidades, por ejemplo tareas, usuarios y así sucesivamente.

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
  - "El backend se divide en controladores, uno por entidad"
stepAt:
  - "Cuando el frontend"
  - "que llega hasta"
  - "la base de datos"
  - "El backend devuelve"
  - "y el frontend la procesa"
  - "Dentro del backend"
cards:
  - icon: 📋
    label: Tareas
  - icon: 👤
    label: Usuarios
  - icon: …
    label: más
items:
  - icon: 🖥️
    label: Frontend
  - icon: ⚙️
    label: Backend
    detail: Controlador
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

Antes de usar nuestra aplicación de tareas, veamos un ejemplo muy pequeño. En una API, quien recibe las peticiones es un controlador: una clase que expone un recurso y tiene métodos que se ejecutan cuando llega una petición. Vamos a crear uno para usuarios. Guarda los nombres en una lista de textos y tiene un método para obtenerlos. Con otro método agregamos un nombre a la lista, y con otro lo quitamos. Cada método responde a una dirección distinta: obtener, crear y remover.

```scene
id: hello-controller
type: code
language: csharp
split: 13
focus:
  - lines: [4]
    at: "quien recibe las peticiones"
  - lines: [2, 3, 4]
    at: "Vamos a crear uno para usuarios"
  - lines: [6]
    at: "Guarda los nombres"
  - lines: [8, 9, 10, 11, 12]
    at: "tiene un método para obtenerlos"
  - lines: [14, 15, 16, 17, 18]
    at: "Con otro método agregamos"
  - lines: [20, 21, 22, 23, 24]
    at: "y con otro lo quitamos"
  - lines: [8, 14, 20]
    at: "Cada método responde a una dirección distinta"
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

### 6. Nuestra API RESTful

Veamos esas convenciones en acción. GET sirve para consultar. POST, para crear una tarea nueva. PUT, para actualizarla. Y DELETE, para borrarla. Las direcciones nos dicen sobre qué tareas vamos a trabajar; el método nos dice qué queremos hacer.

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

### 7. Clona y ejecuta el proyecto

Antes de leer el código, vamos a tenerlo funcionando. Le vamos a pedir a tu agente de inteligencia artificial que clone el proyecto de ejemplo y lo ejecute con Docker. Copia esta instrucción, pégala en el chat de tu agente y espera a que termine. Cuando esté listo, abre Swagger en el navegador: ahí verás el backend en acción.

```scene
id: clonar-proyecto
type: visual
visual: timeline
plain: true
items:
  - icon: 📥
    label: Clonar el proyecto
    detail: Rama Todo-IA
    at: "clone el proyecto de ejemplo"
  - icon: 🐳
    label: Ejecutar con Docker
    detail: build.sh y start.sh
    at: "lo ejecute con Docker"
  - icon: 🌐
    label: Abrir Swagger
    detail: localhost:5080/swagger
    at: "abre Swagger"
```

```exercise
id: clonar-proyecto-prompt
type: prompt-copy
prompt: "Copia esta instrucción y pégala en el chat de tu agente"
buttonLabel: "Copiar instrucción"
copyText: "Clona la rama Todo-IA del repositorio https://github.com/TheScienceOfCode/Ejemplos-IA en una carpeta nueva. Luego construye y ejecuta el proyecto con ./run/build.sh y ./run/start.sh (usa Docker o, si no hay, Podman) y comprueba que Swagger responde en http://localhost:5080/swagger. Al terminar, ejecuta ./run/test.sh para confirmar que la API funciona y dime la dirección para abrir Swagger en el navegador."
explanation: "Instrucción copiada. Pégala en el chat de tu agente y espera a que termine."
```

```exercise
id: clonar-proyecto-check
type: checkpoint
prompt: "Mi agente clonó y ejecutó el proyecto, y veo Swagger en http://localhost:5080/swagger"
explanation: "Perfecto. Ahora sí, veamos el código del backend."
```

### 8. Modelo de datos

#### El proyecto en VS Code

Así se ve el proyecto de nuestra aplicación en VS Code. En el explorador están las carpetas y los archivos. Los modelos de datos viven en la carpeta Models. Abrimos el archivo Tarea.cs y, en el editor, vemos la clase Tarea.

```scene
id: vscode-proyecto
type: visual
visual: vscode
header: TareaApi
focus: 6
stepAt:
  - "En el explorador"
  - "Abrimos el archivo"
  - "en el editor"
items:
  - icon: 📁
    label: TareaApi
    value: 0
  - icon: 📁
    label: Controllers
    value: 1
  - icon: 📄
    label: TareasController.cs
    value: 2
  - icon: 📁
    label: Migrations
    value: 1
  - icon: 📁
    label: Models
    value: 1
  - icon: 📄
    label: Estado.cs
    value: 2
  - icon: 📄
    label: Tarea.cs
    value: 2
  - icon: 📄
    label: appsettings.json
    value: 1
  - icon: 📄
    label: Program.cs
    value: 1
  - icon: 📄
    label: TareaApi.csproj
    value: 1
  - icon: 📄
    label: TareaContext.cs
    value: 1
code: |-
  namespace TareaApi.Models;

  public class Tarea
  {
      public int Id { get; set; }
      public string Titulo { get; set; } = "";
      public string Descripcion { get; set; } = "";
      public Estado Estado { get; set; }
      public DateTime? FechaLimite { get; set; }
  }
```

#### El modelo de datos

Nuestro backend está escrito en C#, un lenguaje orientado a objetos. La clase Tarea es el modelo de datos: describe lo que vamos a persistir, es decir, lo que se guardará en la base de datos. Estado es un enumerado, un tipo que usamos cuando tenemos una cantidad predefinida de estados. En nuestro caso, una tarea puede estar pendiente, en progreso o terminada.

```scene
id: oop-real-project
type: code
language: csharp
split: 9
focus:
  - lines: [1]
    at: "La clase Tarea es el modelo de datos"
  - lines: [3, 4, 5, 6, 7]
    at: "describe lo que vamos a persistir"
  - lines: [10]
    at: "Estado es un enumerado"
  - lines: [12, 13, 14]
    at: "En nuestro caso, una tarea puede estar"
code: |-
  public class Tarea
  {
      public int Id { get; set; }
      public string Titulo { get; set; } = "";
      public string Descripcion { get; set; } = "";
      public Estado Estado { get; set; }
      public DateTime? FechaLimite { get; set; }
  }

  public enum Estado
  {
      Pendiente,
      EnProgreso,
      Terminada
  }
```

#### Un objeto con datos

Veamos un objeto de tipo Tarea con datos. Tiene un título, una descripción y un estado, que empieza como pendiente. Si la tarea avanza, cambiamos su estado a en progreso y, al final, a terminada. Vamos a explorar más a fondo cada una de estas partes.

```scene
id: tarea-objeto
type: code
language: csharp
focus:
  - lines: [1]
    at: "Veamos un objeto de tipo Tarea"
  - lines: [3, 4]
    at: "Tiene un título, una descripción"
  - lines: [5]
    at: "un estado, que empieza como pendiente"
  - lines: [8]
    at: "cambiamos su estado a en progreso"
  - lines: [9]
    at: "al final, a terminada"
code: |-
  var tarea = new Tarea
  {
      Titulo = "Comprar café",
      Descripcion = "Para mañana",
      Estado = Estado.Pendiente
  };

  tarea.Estado = Estado.EnProgreso;
  tarea.Estado = Estado.Terminada;
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

Entity Framework Core, o EF Core, traduce llamadas de C# para interactuar con una base de datos SQL. Así no escribimos SQL a mano: trabajamos con objetos Tarea. Veamos un ejemplo. Fíjate que las operaciones con la base de datos usan await y sus nombres terminan en Async; enseguida veremos por qué. Para guardar, creamos una tarea y la agregamos a la lista de tareas de la base de datos; luego guardamos los cambios. Para editar, buscamos la tarea, cambiamos sus propiedades y volvemos a guardar los cambios. Para borrar, la quitamos de la lista y guardamos los cambios. Y para consultar, filtramos las tareas con una condición, por ejemplo, las que están pendientes.

```scene
id: ef-intro
type: code
language: csharp
split: 10
focus:
  - lines: [2, 3, 4]
    at: "Para guardar"
  - lines: [7, 8, 9]
    at: "Para editar"
  - lines: [12, 13]
    at: "Para borrar"
  - lines: [16, 17, 18]
    at: "Y para consultar"
code: |-
  // Guardar
  var nueva = new Tarea { Titulo = "Comprar café" };
  db.Tareas.Add(nueva);
  await db.SaveChangesAsync();

  // Editar
  var tarea = await db.Tareas.FindAsync(1);
  tarea.Estado = Estado.Terminada;
  await db.SaveChangesAsync();

  // Borrar
  db.Tareas.Remove(tarea);
  await db.SaveChangesAsync();

  // Consultar
  var pendientes = await db.Tareas
      .Where(t => t.Estado == Estado.Pendiente)
      .ToListAsync();
```

### 11. ¿Por qué async?

En las consultas verás que los métodos terminan en Async y se usan con await. ¿Por qué? Consultar la base de datos toma tiempo, y mientras tanto el servidor no tiene nada más que hacer con esa petición. Sin async, el hilo que atiende la petición se queda esperando, bloqueado, y no puede atender a nadie más. Con async, ese hilo queda libre mientras espera y puede atender otras peticiones; cuando llega la respuesta de la base de datos, continúa donde se quedó. En términos de escalabilidad, significa que con los mismos recursos el servidor puede atender a muchas más personas al mismo tiempo.

```scene
id: async-escalabilidad
type: visual
visual: async-lanes
steps:
  - "Mismos recursos, más personas atendidas al mismo tiempo"
stepAt:
  - "Sin async"
  - "Con async"
  - "En términos de escalabilidad"
items:
  - icon: ⏳
    label: Sin async
    detail: El hilo espera sin hacer nada
  - icon: ⚡
    label: Con async
    detail: El hilo atiende a otros mientras espera
```

### 12. Consultas y comandos

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

### 13. Migraciones: cambiar la base de datos

¿Y si mañana queremos guardar una fecha de vencimiento para cada tarea? No basta con agregar ese dato al código: también necesitamos modificar la estructura de la base de datos. Para eso sirven las migraciones. Nuestro ejemplo ya tiene una que crea las tareas y otra que agrega la fecha, conservando los datos anteriores. Ahora te toca: abre la carpeta Migrations de tu proyecto y revisa sus archivos. Después consulta con tu agente cómo crear una migración nueva.

```scene
id: ef-migrations
type: visual
visual: timeline
plain: true
items:
  - icon: 📋
    label: InitialCreate
    detail: "Crea Id, Titulo, Descripcion y Estado"
  - icon: 📅
    label: AddFechaLimite
    detail: "Agrega FechaLimite a la tabla existente"
  - icon: ✅
    label: Resultado
    detail: "La tabla evoluciona sin borrar las tareas"
```

```exercise
id: migraciones-agente
type: prompt-copy
prompt: "Copia esta instrucción y pégala en el chat de tu agente"
buttonLabel: "Copiar instrucción"
copyText: "En el proyecto src/back/TareaApi, revisa la carpeta Migrations: explícame qué hace cada migración (InitialCreate y AddFechaLimite) y para qué sirven los archivos Designer y el Snapshot. Después explícame, paso a paso, cómo crear una migración nueva con EF Core, por ejemplo para agregar una propiedad Prioridad a Tarea, y qué comandos usaría en este proyecto. No cambies nada todavía: solo explícame."
explanation: "Instrucción copiada. Pégala en el chat de tu agente y lee con calma su explicación."
```

```exercise
id: migraciones-check
type: checkpoint
prompt: "Revisé la carpeta Migrations y entiendo cómo se crea una migración nueva"
explanation: "Muy bien. Más adelante practicarás creando una migración tuya."
```

### 14. El controlador: la puerta de entrada

#### La clase del controlador

Ya tenemos las piezas. El controlador es la puerta de entrada de nuestra API: recibe una petición HTTP, elige qué operación ejecutar y devuelve una respuesta. La ruta indica la dirección base de todos sus métodos. Y el constructor recibe el acceso a la base de datos, así puede consultar o modificar tareas sin encargarse de preparar la conexión.

```scene
id: controller-entry
type: code
language: csharp
focus:
  - lines: [3]
    at: "El controlador es la puerta de entrada"
  - lines: [2]
    at: "La ruta indica"
  - lines: [5, 7, 8, 9, 10]
    at: "el constructor recibe"
code: |-
  [ApiController]
  [Route("api/tareas")]
  public class TareasController : ControllerBase
  {
      private readonly TareaContext _db;

      public TareasController(TareaContext db)
      {
          _db = db;
      }

      // ... los métodos, uno por cada operación
  }
```

#### GET: consultar

Para consultar usamos GET. El primer método devuelve la lista de tareas. El segundo busca una tarea por su identificador y, si no existe, responde que no se encontró.

```scene
id: controller-get
type: code
language: csharp
focus:
  - lines: [1, 2, 3, 4, 5]
    at: "El primer método devuelve la lista"
  - lines: [7, 8, 9, 10, 11, 12, 13]
    at: "El segundo busca una tarea"
  - lines: [11]
    at: "responde que no se encontró"
code: |-
      [HttpGet]
      public async Task<ActionResult<List<Tarea>>> GetAll()
      {
          return await _db.Tareas.ToListAsync();
      }

      [HttpGet("{id}")]
      public async Task<ActionResult<Tarea>> Get(int id)
      {
          var tarea = await _db.Tareas.FindAsync(id);
          if (tarea == null) return NotFound();
          return tarea;
      }
```

#### POST: crear

Para crear usamos POST. El método recibe la tarea que viene en el cuerpo de la petición, la agrega a la base de datos, guarda los cambios y responde con el código 201, creado, junto con la tarea nueva.

```scene
id: controller-post
type: code
language: csharp
focus:
  - lines: [2]
    at: "El método recibe la tarea"
  - lines: [5]
    at: "la agrega a la base de datos"
  - lines: [6]
    at: "guarda los cambios"
  - lines: [7]
    at: "responde con el código 201"
code: |-
      [HttpPost]
      public async Task<ActionResult<Tarea>> Create(Tarea tarea)
      {
          tarea.Id = 0;
          _db.Tareas.Add(tarea);
          await _db.SaveChangesAsync();
          return CreatedAtAction(nameof(Get), new { id = tarea.Id }, tarea);
      }
```

#### PUT: actualizar

Para actualizar usamos PUT, con el identificador de la tarea. Buscamos la tarea y, si no existe, respondemos que no se encontró. Si existe, copiamos los valores nuevos, guardamos los cambios y respondemos sin contenido.

```scene
id: controller-put
type: code
language: csharp
focus:
  - lines: [4]
    at: "Buscamos la tarea"
  - lines: [5]
    at: "si no existe"
  - lines: [7, 8, 9, 10]
    at: "copiamos los valores nuevos"
  - lines: [11]
    at: "guardamos los cambios"
  - lines: [12]
    at: "respondemos sin contenido"
code: |-
      [HttpPut("{id}")]
      public async Task<IActionResult> Update(int id, Tarea tarea)
      {
          var existing = await _db.Tareas.FindAsync(id);
          if (existing == null) return NotFound();

          existing.Titulo = tarea.Titulo;
          existing.Descripcion = tarea.Descripcion;
          existing.Estado = tarea.Estado;
          existing.FechaLimite = tarea.FechaLimite;
          await _db.SaveChangesAsync();
          return NoContent();
      }
```

#### DELETE: borrar

Para borrar usamos DELETE. Buscamos la tarea y, si no existe, respondemos que no se encontró. Si existe, la quitamos de la base de datos, guardamos los cambios y respondemos sin contenido. Así, el controlador conecta cada petición HTTP con EF Core.

```scene
id: controller-delete
type: code
language: csharp
focus:
  - lines: [4]
    at: "Buscamos la tarea"
  - lines: [5]
    at: "si no existe"
  - lines: [7]
    at: "la quitamos de la base de datos"
  - lines: [8]
    at: "guardamos los cambios"
  - lines: [9]
    at: "respondemos sin contenido"
code: |-
      [HttpDelete("{id}")]
      public async Task<IActionResult> Delete(int id)
      {
          var tarea = await _db.Tareas.FindAsync(id);
          if (tarea == null) return NotFound();

          _db.Tareas.Remove(tarea);
          await _db.SaveChangesAsync();
          return NoContent();
      }
```

### 15. Consultar tareas: de Swagger a la respuesta

#### Del navegador a la base de datos

Miremos una operación completa. Desde Swagger, que corre en el navegador, pedimos la lista de tareas. El controlador consulta la base de datos mediante EF Core, recibe los datos y los devuelve como respuesta. Swagger la muestra en pantalla.

```scene
id: swagger-get-flujo
type: visual
visual: request-flow
steps:
  - "Swagger envía una petición GET"
  - "El controlador ejecuta GetAll() y consulta la base de datos"
  - "La base de datos entrega las tareas"
  - "El controlador devuelve la respuesta"
  - "Swagger muestra el resultado"
stepAt:
  - "pedimos la lista de tareas"
  - "El controlador consulta la base de datos"
  - "recibe los datos"
  - "los devuelve como respuesta"
  - "Swagger la muestra"
items:
  - icon: 🌐
    label: Navegador
    detail: Swagger
  - icon: 🎛️
    label: Controlador
    detail: GetAll()
  - icon: 💾
    label: Base de datos
    detail: Tabla Tareas
```

#### La respuesta del servidor

En Swagger pulsamos Execute. El servidor responde con el código 200, que significa que todo salió bien, y con las tareas en formato JSON, tal como lo recibiría cualquier programa que utilice esta API.

```scene
id: swagger-get
type: visual
visual: swagger-mock
stage: request-response
header: "GET /api/tareas"
request:
  method: GET
  path: /api/tareas
response:
  status: 200
  json: |-
    [
      {
        "id": 1,
        "titulo": "Comprar café",
        "descripcion": "",
        "estado": "Pendiente",
        "fechaLimite": null
      }
    ]
```

#### ¿Qué es JSON?

JSON es un formato de texto para representar datos, que entienden tanto las personas como los programas. Una lista va entre corchetes. Cada objeto va entre llaves, y está formado por pares: un nombre y su valor. Aquí tenemos una tarea con su identificador, su título, su descripción, su estado y su fecha límite, que por ahora no tiene valor.

```scene
id: json-explicado
type: code
language: json
focus:
  - lines: [1, 9]
    at: "Una lista va entre corchetes"
  - lines: [2, 8]
    at: "Cada objeto va entre llaves"
  - lines: [3]
    at: "un nombre y su valor"
  - lines: [3, 4, 5, 6]
    at: "Aquí tenemos una tarea"
  - lines: [7]
    at: "que por ahora no tiene valor"
code: |-
  [
    {
      "id": 1,
      "titulo": "Comprar café",
      "descripcion": "",
      "estado": "Pendiente",
      "fechaLimite": null
    }
  ]
```

### 16. Crear tareas: enviar datos

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
    { "titulo": "Comprar café", "descripcion": "Para mañana", "estado": "Pendiente" }
response:
  status: 201
  json: |-
    { "id": 1, "titulo": "Comprar café", "descripcion": "Para mañana", "estado": "Pendiente", "fechaLimite": null }
```

### 17. Cambiar el estado de una tarea

La tarea ya existe, pero ahora estamos trabajando en ella. Podemos enviar una petición PUT con el mismo identificador y cambiar su estado a en progreso. El controlador busca la tarea, modifica sus datos y guarda el cambio. Si volvemos a consultarla, veremos el nuevo estado.

```scene
id: swagger-put
type: visual
visual: swagger-mock
stage: request-response
header: "PUT /api/tareas/1"
show: "Simular seleccionar PUT, escribir id 1 y enviar el JSON. Mostrar la tarjeta de la tarea cambiando visualmente de Pendiente a EnProgreso. Swagger devuelve 204 No Content; después ejecutar GET /api/tareas/1 para verificar el nuevo estado."
request:
  method: PUT
  path: /api/tareas/1
  json: |-
    { "titulo": "Comprar café", "descripcion": "Para mañana", "estado": "EnProgreso" }
response:
  status: 204
followup:
  method: GET
  path: /api/tareas/1
  status: 200
  json: |-
    { "id": 1, "titulo": "Comprar café", "descripcion": "Para mañana", "estado": "EnProgreso", "fechaLimite": null }
```

### 18. Te toca: probar Swagger y modificar el código

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
explanation: "Pista: puedes usar OrderBy(t => t.Titulo) antes de ToListAsync(). Prueba creando dos tareas en orden inverso al alfabético."
```

```exercise
id: practice-enum
type: checkpoint
prompt: "Agregué el estado Cancelada al enum Estado y comprobé que puedo usarlo al actualizar una tarea."
explanation: "Busca los estados existentes en Estado.cs; luego prueba desde Swagger con el nuevo valor."
```

### 19. Reto: agrega un responsable a las tareas

Ahora un reto de verdad. Queremos que cada tarea tenga un responsable: la persona encargada de ella. Para eso necesitamos una tabla nueva, Responsable, con un identificador y un nombre. Y necesitamos una relación entre las dos tablas: un responsable puede tener muchas tareas, y cada tarea pertenece a un responsable. Esto toca varias piezas: el modelo, el contexto, una migración y el controlador. No lo vas a escribir a mano: le vas a pedir a tu agente que lo haga y que te explique cada paso. Copia esta instrucción, pégala en el chat y revisa con calma qué archivos cambia, qué contiene la migración y qué pruebas ejecuta.

```scene
id: reto-responsable
type: visual
visual: table-relation
steps:
  - "Un responsable tiene muchas tareas"
stepAt:
  - "una relación entre las dos tablas"
items:
  - icon: 👤
    label: Responsable
    at: "una tabla nueva"
    steps:
      - "Id (PK)"
      - "Nombre"
  - icon: 📋
    label: Tarea
    at: "cada tarea pertenece"
    steps:
      - "Id (PK)"
      - "Titulo"
      - "Descripcion"
      - "Estado"
      - "FechaLimite"
      - "ResponsableId (FK)"
```

```exercise
id: reto-responsable-prompt
type: prompt-copy
prompt: "Copia esta instrucción y pégala en el chat de tu agente"
buttonLabel: "Copiar instrucción"
copyText: "Quiero que cada tarea tenga un responsable. Modifica la API de src/back/TareaApi así: (1) crea la clase Responsable con Id (entero) y Nombre (texto); (2) crea la relación: un responsable tiene muchas tareas y cada Tarea tiene un ResponsableId y una propiedad Responsable (el responsable debe ser opcional para no romper las tareas que ya existen); (3) agrega la tabla Responsables al contexto TareaContext y crea una migración nueva de EF Core llamada AddResponsable; (4) crea un ResponsablesController para listar y crear responsables, y haz que al crear o actualizar una tarea se pueda indicar su ResponsableId; (5) reconstruye con ./run/build.sh, inicia con ./run/start.sh y prueba el resultado: crea un responsable, asígnaselo a una tarea y consulta la tarea; ejecuta también ./run/test.sh. Explícame cada paso y por qué lo haces, muéstrame los archivos que cambiaste y qué contiene la migración."
explanation: "Instrucción copiada. Pégala en el chat de tu agente y lee con calma su explicación mientras trabaja."
```

```exercise
id: reto-responsable-clave
type: multiple-choice
prompt: "¿Qué columna enlaza una tarea con su responsable?"
choices:
  - "ResponsableId, una clave foránea en la tabla de tareas"
  - "Un Id nuevo en la tabla de responsables"
  - "El Nombre del responsable, copiado en cada tarea"
answer: 0
explanation: "La clave foránea ResponsableId, en Tarea, apunta al Id del Responsable. Así muchas tareas pueden compartir el mismo responsable."
```

```exercise
id: reto-responsable-check
type: checkpoint
prompt: "Mi agente agregó la relación y la migración, y comprobé en Swagger que puedo asignar un responsable a una tarea."
explanation: "Excelente: modificaste el modelo, la base de datos y la API con ayuda de tu agente, y lo verificaste tú mismo."
```
