---
title: "Lección 2: Entender el backend"
courseTitle: "Aprende a\nProgramar con IA"
language: es
objectives:
  - Entender cómo se comunican los programas mediante una API HTTP
  - Reconocer clases, objetos, propiedades, enums, constructores y métodos
  - Comprender cómo el backend consulta y guarda tareas con EF Core
  - Leer un controlador real y hacer cambios pequeños que funcionen
prerequisites:
  - Lección 1
  - Editor con agente de programación y Docker
---

# Lección 2 — Entender el backend

**Proyecto:** Aprende a Programar con IA  
**Código de ejemplo:** https://github.com/TheScienceOfCode/Ejemplos-IA/tree/Todo-IA  
**Referencia de formato:** https://github.com/TheScienceOfCode/Programar-con-IA/blob/main/lessons/session-1/INDEX.md  
**Público:** personas que construyeron una aplicación con IA, pero apenas empiezan a leer código.  
**Objetivo:** entender qué sucede desde que pedimos una tarea hasta que el backend la consulta o guarda, y poder modificar ese recorrido.

## Notas de producción

- Cada `###` es una pantalla. El texto que precede a `scene` es **la narración**, escrita para escucharse, no para leerse como documentación.
- **No narrar nombres de archivos, rutas, firmas de métodos ni comandos.** Esos datos se muestran en pantalla al abrir el código, cuando corresponda.
- Primero explicar una idea cotidiana; después mostrar cómo aparece en nuestro código. Mostrar **pocas líneas** cada vez.
- `scene` indica lo que se ve; `exercise`, la pregunta o práctica. Las escenas de código toman sus fragmentos del repositorio real; los ejemplos nuevos deben señalarse como tales.
- **No introducir frontend ni patrones adicionales.** Esta lección es solo sobre el backend.
- Dejar que el espectador piense y pruebe los ejercicios antes de mostrar pistas o soluciones.

## Partes

### 1. ¿Qué vamos a entender?

En la primera lección construimos una aplicación con ayuda de la inteligencia artificial. Ahora vamos a empezar a entender el código que escribe por nosotros. Para hacerlo, usaremos una aplicación mucho más pequeña: una lista de tareas. Podemos agregar una tarea, consultar las que tenemos, cambiar su estado o borrarla. Hoy nos concentraremos en la parte que recibe esas órdenes y guarda la información: el backend.

```scene
id: introduction
type: visual
visual: backend
plain: true
steps:
  - Crear una tarea
  - Ver las tareas guardadas
  - Marcar una como terminada
  - Borrar una tarea
items:
  - icon: 🖥️
    label: Backend
    detail: Recibe las órdenes y maneja los datos
  - icon: 💾
    label: Base de datos
    detail: Conserva nuestras tareas
```
```exercise
id: intro-question
type: multiple-choice
prompt: Si queremos guardar una tarea para encontrarla mañana, ¿qué parte debe encargarse de almacenarla?
choices:
  - El backend, utilizando una base de datos
  - El botón que pulsamos
  - La pantalla de Swagger
answer: 0
explanation: La pantalla solicita una acción; el backend la procesa y guarda los datos.
```

### 2. ¿Qué es una API?

Imagina que quieres consultar tus tareas desde el computador, pero también desde el teléfono. No tendría sentido construir un sistema de tareas diferente para cada dispositivo. Lo que necesitamos es que ambos puedan comunicarse con el mismo programa.

Una **API** es precisamente eso: una forma definida de pedirle cosas a otro programa. Puede ofrecer operaciones como «muéstrame las tareas» o «guarda esta nueva tarea». Las API existen en muchos tipos de programas; la nuestra se usa a través de la web.

```scene
id: api-concept
type: visual
visual: backend
plain: true
steps:
  - 'Computador: Muéstrame las tareas'
  - 'API: recibe la solicitud'
  - 'Backend: busca las tareas'
  - 'API: devuelve el resultado'
items:
  - icon: 💻
    label: Computador
  - icon: 📱
    label: Teléfono
  - icon: ⚙️
    label: La misma API
    detail: Ambos pueden pedirle operaciones
```
```exercise
id: api-question
type: multiple-choice
prompt: ¿Por qué una API permite que distintos programas utilicen el mismo backend?
choices:
  - Porque define cómo pedir operaciones y recibir resultados
  - Porque instala una copia de la base de datos en cada dispositivo
  - Porque sustituye al sistema operativo
answer: 0
explanation: Los programas conocen cómo comunicarse con la API, sin tener que conocer su funcionamiento interno.
```

### 3. HTTP: cómo se hablan los programas

Cuando abres una página web, tu navegador le hace una petición a un servidor y espera una respuesta. Para entenderse utilizan unas reglas comunes llamadas **HTTP**. Nuestras tareas funcionan de manera parecida.

Por ejemplo, podemos pedir la tarea número cinco. El servidor busca esa tarea y responde. Si la encuentra, devuelve su información; si no existe, nos lo indica. Por eso, una respuesta no solo trae datos: también nos dice si la operación salió bien o qué ocurrió.

```scene
id: http-exchange
type: visual
visual: timeline
plain: true
items:
  - icon: 📤
    label: Petición
    detail: Quiero consultar la tarea 5
  - icon: ⚙️
    label: Servidor
    detail: Busca esa tarea
  - icon: ✅
    label: Si existe
    detail: 200 OK y los datos
  - icon: ❓
    label: Si no existe
    detail: 404 Not Found
```

**Nota visual:** después de la explicación, mostrar brevemente la petición real `GET /api/todos/5` y la respuesta. No leer la ruta en voz alta.

```exercise
id: http-question
type: multiple-choice
prompt: Pides una tarea que no existe. ¿Qué debería indicar la respuesta?
choices:
  - Que no se encontró
  - Que se creó una nueva
  - Que se borraron todas las tareas
answer: 0
explanation: HTTP incluye códigos de respuesta; 404 significa que no se encontró el recurso solicitado.
```

### 4. REST: organizar lo que podemos pedir

Con HTTP podemos hacer distintas clases de peticiones. Y cuando seguimos el estilo **REST**, organizamos esas peticiones alrededor de las cosas que maneja nuestra aplicación. En este caso, la cosa principal es una tarea.

Así, **GET** se utiliza para consultar, **POST** para crear, **PUT** para actualizar y **DELETE** para borrar. No necesitamos inventar una forma distinta de hablar con cada aplicación: estas operaciones siguen convenciones que muchos programas comparten.

```scene
id: rest-operations
type: visual
visual: timeline
plain: true
items:
  - icon: 🔎
    label: GET
    detail: Consultar tareas
  - icon: ➕
    label: POST
    detail: Crear una tarea
  - icon: ✏️
    label: PUT
    detail: Actualizarla
  - icon: 🗑️
    label: DELETE
    detail: Borrarla
```

**Nota visual:** abrir Swagger y señalar las operaciones existentes. Solo en pantalla: `GET /api/todos`, `GET /api/todos/{id}`, `POST /api/todos`, `PUT /api/todos/{id}` y `DELETE /api/todos/{id}`. Explicar que Swagger es una pantalla para explorar y probar la API; no es la API en sí.

```exercise
id: rest-question
type: multiple-choice
prompt: Una tarea ya existe, pero quieres marcarla como terminada. ¿Qué operación corresponde?
choices:
  - PUT, para actualizarla
  - GET, para consultarla
  - DELETE, para eliminarla
answer: 0
explanation: PUT se utiliza en esta API para actualizar una tarea existente.
```

### 5. Clases, objetos y propiedades

Ahora sí, miremos cómo se representa una tarea en C#. Antes de guardar algo, el programa necesita saber qué información tiene. Una **clase** sirve para describir esa estructura.

Nuestra clase de tarea tiene un título, una descripción, un estado y una fecha opcional. Cada tarea concreta que creamos es un **objeto** de esa clase. Por ejemplo, «Comprar café» es una tarea; «Llamar al médico» es otra. Tienen la misma estructura, pero distintos valores.

Los datos de un objeto suelen llamarse **atributos**; en este código C# los declaramos como **propiedades**. Cada propiedad tiene un tipo: texto, número, fecha, etcétera.

```scene
id: classes-objects
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

**Nota visual:** resaltar `class Todo`, luego dos objetos imaginarios: «Comprar café» y «Llamar al médico». Después señalar `string` como texto, `int` como entero y `?` como valor opcional. Mostrar `get; set;` como la posibilidad de leer o modificar una propiedad, sin detenerse en la sintaxis.

```exercise
id: class-question
type: multiple-choice
prompt: Si creas dos tareas con títulos distintos, ¿qué tienen en común?
choices:
  - Son dos objetos de la misma clase Todo
  - Son dos clases nuevas
  - Deben tener el mismo título
answer: 0
explanation: La clase define qué datos tiene una tarea; cada objeto tiene sus propios valores.
```

### 6. Enums: elegir entre opciones conocidas

No queremos que una tarea tenga cualquier estado inventado. Queremos saber si está pendiente, en progreso o terminada. Para eso existe un **enum**: una lista de opciones permitidas que podemos utilizar desde el código.

Así, en vez de escribir el estado de cualquier manera y equivocarnos, usamos un valor conocido. Si más adelante necesitamos admitir tareas canceladas, podemos agregar otra opción.

```scene
id: enum-intro
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
id: enum-question
type: multiple-choice
prompt: ¿Qué ventaja tiene usar un enum para el estado de una tarea?
choices:
  - Que los estados posibles están definidos y tienen nombres claros
  - Que cada tarea se guarda automáticamente
  - Que no necesitamos una base de datos
answer: 0
explanation: Un enum evita que trabajemos con estados arbitrarios o escritos de maneras diferentes.
```

### 7. Métodos y constructores: lo que hace una clase

Una clase no solo puede guardar datos: también puede tener **métodos**. Un método es una acción definida en el código. Por ejemplo, nuestro controlador tiene un método para buscar todas las tareas y otro para crear una nueva.

Hay un método especial llamado **constructor**. Se utiliza cuando se crea un objeto y sirve para prepararlo. Puede recibir información o herramientas que ese objeto necesitará. Más adelante veremos un constructor que recibe acceso a la base de datos. Por ahora, quédate con esta diferencia: las propiedades describen datos; los métodos realizan acciones; el constructor prepara el objeto al crearlo.

```scene
id: methods-constructors
type: code
language: csharp
file: src/back/TodoApi/Controllers/TodosController.cs
code: |-
  // Constructor: prepara el controlador al crearlo
  public TodosController(TodoContext db)
  {
      _db = db;
  }

  // Método: atiende una petición para consultar todas las tareas
  public async Task<ActionResult<List<Todo>>> GetAll()
  {
      return await _db.Todos.ToListAsync();
  }
```

**Nota visual:** este fragmento anticipa el controlador. Resaltar solamente los nombres `TodosController` y `GetAll`. Aclarar en pantalla que un constructor tiene el nombre de la clase, mientras que los métodos tienen nombres de acciones. No explicar todavía `async`, `Task` ni genéricos.

```exercise
id: method-question
type: multiple-choice
prompt: ¿Qué diferencia hay entre una propiedad y un método?
choices:
  - Una propiedad representa un dato y un método realiza una acción
  - Una propiedad guarda todas las tareas y un método solo guarda textos
  - Son dos nombres para lo mismo
answer: 0
explanation: Por ejemplo, Title es una propiedad; GetAll es un método que consulta tareas.
```

### 8. Inyección de dependencias: recibir lo que necesitamos

Imagina que el controlador tiene que consultar las tareas. Para hacerlo necesita una herramienta que le permita acceder a la base de datos. Podría intentar construir esa herramienta por su cuenta, pero hay una alternativa más sencilla: **recibirla ya preparada**.

A eso lo llamamos **inyección de dependencias**. La aplicación configura las herramientas disponibles y se las entrega a las clases que las necesitan. Nuestro controlador dice, a través de su constructor, que necesita acceso a los datos. Así puede concentrarse en atender las peticiones, en vez de encargarse de crear esa conexión.

```scene
id: dependency-injection
type: visual
visual: backend
plain: true
steps:
  - La aplicación prepara el acceso a los datos
  - El controlador lo pide en su constructor
  - ASP.NET Core se lo entrega
  - El controlador puede consultar y guardar tareas
```

**Nota visual:** conectar dos fragmentos reales. En `Program.cs`, `builder.Services.AddDbContext<TodoContext>(...)`. En `TodosController.cs`, `public TodosController(TodoContext db) { _db = db; }`. Mostrar las líneas; no narrar los nombres técnicos. Explicar que `TodoContext` es la herramienta de datos que veremos a continuación.

```exercise
id: di-question
type: multiple-choice
prompt: Si el controlador necesita acceso a la base de datos, ¿qué hace la inyección de dependencias?
choices:
  - Se lo entrega cuando se crea el controlador
  - Convierte el controlador en una base de datos
  - Obliga al navegador a instalar SQLite
answer: 0
explanation: La aplicación prepara y proporciona las dependencias que sus componentes necesitan.
```

### 9. EF Core: trabajar con datos desde C#

Ya sabemos cómo describir una tarea, pero falta guardarla para que no desaparezca cuando apaguemos el programa. Para eso tenemos una base de datos. Piensa en una tabla: cada fila sería una tarea y cada columna, uno de sus datos.

**Entity Framework Core**, o **EF Core**, nos permite trabajar con esas tareas usando objetos y código C#, sin tener que escribir manualmente una instrucción SQL para cada operación. En nuestro ejemplo utiliza una base de datos SQLite. Y la clase que organiza ese acceso se llama `TodoContext`: es precisamente la herramienta que recibe el controlador.

```scene
id: efcore-bridge
type: visual
visual: backend
plain: true
steps:
  - 'Objeto Todo: título, descripción, estado'
  - EF Core lo relaciona con los datos almacenados
  - 'Tabla Todos: una fila por tarea'
  - SQLite conserva las tareas
```

**Nota visual:** abrir `TodoContext.cs` y señalar `DbSet<Todo> Todos` como el conjunto de tareas. Si se muestra el archivo, no leer la declaración completa en la narración.

```exercise
id: efcore-question
type: multiple-choice
prompt: ¿Para qué nos sirve EF Core en este proyecto?
choices:
  - Para consultar y modificar las tareas guardadas desde C#
  - Para dibujar botones
  - Para convertir HTTP en una imagen
answer: 0
explanation: EF Core conecta nuestro código con los datos almacenados en SQLite.
```

### 10. Consultas: encontrar lo que buscamos

Supongamos que guardamos diez tareas. Ahora queremos verlas todas, buscar una en particular o mostrar únicamente las pendientes. Son tres formas de hacer una **consulta**: leer datos sin modificarlos.

En C# podemos expresar esas búsquedas con instrucciones bastante descriptivas. Una obtiene la lista completa, otra busca por identificador y otra filtra según una condición. No hace falta memorizar cada símbolo; lo importante es reconocer qué se está pidiendo. Enseguida vas a modificar una de esas consultas.

```scene
id: ef-queries
type: code
language: csharp
file: src/back/TodoApi/Controllers/TodosController.cs
code: |-
  // Obtener todas las tareas (código real)
  await _db.Todos.ToListAsync();

  // Buscar una tarea por su identificador (código real)
  await _db.Todos.FindAsync(id);

  // Ejemplo nuevo: obtener solo las pendientes
  await _db.Todos
      .Where(t => t.Status == Status.Pending)
      .ToListAsync();
```

**Nota visual:** mostrar tres tarjetas «Todas», «La número 5», «Solo pendientes» que se relacionan con cada fragmento. Explicar en pantalla que `Where` filtra, y que `await` espera el resultado de una operación que puede tardar; no desarrollar programación asíncrona en esta lección.

```exercise
id: query-question
type: multiple-choice
prompt: Tienes diez tareas y quieres ver solo las pendientes. ¿Necesitas modificar la base de datos?
choices:
  - No. Necesitas una consulta que filtre por estado
  - Sí. Debes borrar las demás tareas
  - Sí. Hay que crear una base de datos nueva
answer: 0
explanation: Consultar o filtrar datos no requiere modificarlos.
```

### 11. Comandos: guardar cambios

Consultar es una cosa; **cambiar información** es otra. Cuando creamos una tarea, el backend la agrega. Cuando la terminamos, cambia su estado. Cuando la borramos, la elimina.

Hay un detalle importante: hacer esos cambios en los objetos del programa no basta. Necesitamos confirmarlos en la base de datos para que queden guardados. En EF Core eso se hace con una operación de guardar cambios. Si olvidamos ese paso, podemos pensar que modificamos algo, pero el cambio no queda almacenado.

```scene
id: ef-writes
type: code
language: csharp
file: src/back/TodoApi/Controllers/TodosController.cs
code: |-
  // Crear
  _db.Todos.Add(todo);
  await _db.SaveChangesAsync();

  // Actualizar una tarea que ya encontramos
  existing.Status = todo.Status;
  await _db.SaveChangesAsync();

  // Borrar
  _db.Todos.Remove(todo);
  await _db.SaveChangesAsync();
```

**Nota visual:** primero representar las acciones con una tarea «Comprar café»; después resaltar las líneas de C#. Señalar que actualizar no requiere llamar a `Update` aquí: EF Core detecta los cambios en el objeto que está siguiendo.

```exercise
id: write-question
type: multiple-choice
prompt: Cambias el estado de una tarea en el código, pero no confirmas los cambios. ¿Qué puede pasar?
choices:
  - Que el cambio no quede guardado en la base de datos
  - Que se guarde obligatoriamente igual
  - Que se borren automáticamente las demás tareas
answer: 0
explanation: SaveChangesAsync confirma las modificaciones pendientes en la base de datos.
```

### 12. Migraciones: cuando nuestros datos evolucionan

Al principio, nuestras tareas solo tenían título, descripción y estado. Después decidimos agregarles una fecha de vencimiento. Cambiar la clase en C# es fácil, pero la base de datos también necesita espacio para guardar ese dato nuevo.

Para eso sirven las **migraciones**: describen cómo debe cambiar la estructura de la base de datos de una versión a otra. Nuestro ejemplo ya trae una migración que crea la tabla y otra que agrega la fecha. Podemos actualizar la estructura sin empezar de cero ni perder las tareas anteriores.

```scene
id: migrations
type: visual
visual: timeline
plain: true
items:
  - icon: 📋
    label: Primera versión
    detail: Título, descripción y estado
  - icon: 📅
    label: Necesidad nueva
    detail: Agregar fecha de vencimiento
  - icon: 🛠️
    label: Migración
    detail: Agrega la columna a la tabla existente
  - icon: 💾
    label: Resultado
    detail: Seguimos teniendo nuestras tareas guardadas
```

**Nota visual:** enseñar las migraciones reales `InitialCreate` y `AddDueDate`; luego señalar en `Program.cs` que las pendientes se aplican al arrancar. Mostrar que los datos se guardan en un volumen Docker que permanece cuando detenemos y reiniciamos el backend.

```exercise
id: migrations-question
type: multiple-choice
prompt: Agregas una nueva propiedad a las tareas y necesitas guardarla. ¿Para qué creas una migración?
choices:
  - Para adaptar la estructura de la base de datos sin borrar lo que ya existe
  - Para cambiar el color de la aplicación
  - Para instalar de nuevo el navegador
answer: 0
explanation: Las migraciones permiten que la base de datos evolucione junto con nuestro código.
```

### 13. El controlador: todas las piezas juntas

Ya conocemos las piezas. Ahora sigamos una petición real. Alguien pide la lista de tareas. El servidor recibe esa petición HTTP y el **controlador** decide qué método debe ejecutarse. Ese método usa el acceso a datos que recibió en su constructor, consulta las tareas y devuelve el resultado.

Si pedimos una tarea específica y no existe, el controlador responde que no la encontró. Si pedimos crear una, la guarda y responde que fue creada. Eso es lo que hace el controlador: conectar las peticiones que llegan por la API con las operaciones del programa.

```scene
id: controller-flow
type: visual
visual: backend
plain: true
steps:
  - El cliente pide ver las tareas
  - HTTP lleva la petición al backend
  - El controlador recibe la petición
  - Consulta las tareas mediante EF Core
  - La API devuelve los resultados al cliente
```

**Nota visual:** abrir `TodosController.cs` y recorrer, en este orden, sin leer rutas ni sintaxis en voz alta:

1. `[Route("api/todos")]`: dirección donde recibe peticiones.
2. Constructor `TodosController(TodoContext db)`: recibe la dependencia y la guarda en `_db`.
3. `[HttpGet]` y `GetAll()`: reconoce una petición de consulta y obtiene los datos.
4. `[HttpGet("{id}")]` y `Get(int id)`: busca una sola tarea; si no existe, responde `NotFound()`.
5. `Create`, `Update` y `Delete`: señalar brevemente que utilizan las operaciones de EF Core vistas anteriormente.

**Aclaración visual:** los corchetes `[HttpGet]` son «atributos» de C# para identificar el tipo de petición. No confundirlos con las propiedades del objeto `Todo`.

```exercise
id: controller-question
type: multiple-choice
prompt: El cliente pide todas las tareas. ¿Quién recibe la petición y utiliza EF Core para buscarlas?
choices:
  - El controlador
  - El enum Status
  - La migración AddDueDate
answer: 0
explanation: El controlador atiende la petición y utiliza el contexto de datos que recibió por inyección de dependencias.
```

### 14. Ahora te toca modificar el backend

Ya no estamos mirando código desconocido. Sabemos qué representa una tarea, dónde se consulta, cómo se guarda y qué parte recibe las peticiones. Hagamos tres cambios pequeños. Intenta escribirlos tú primero. Puedes pedirle al agente que te explique una línea o te ayude con un error, pero verifica personalmente que cada cambio funcione.

#### Ejercicio 1 — Ordenar las tareas

**Objetivo:** que la lista de tareas aparezca en orden alfabético por título.

**Dónde mirar:** método `GetAll()` del controlador.

**Pista:** en una consulta de EF Core, `OrderBy(t => t.Title)` permite ordenar por título.

**Cómo comprobarlo:** crea las tareas «Zanahorias» y «Arroz», en ese orden. Al consultar la lista, «Arroz» debería aparecer primero.

```scene
id: exercise-sort
type: code
language: csharp
file: src/back/TodoApi/Controllers/TodosController.cs
code: |-
  // Código actual
  return await _db.Todos.ToListAsync();

  // Tu reto: ordenar por Title antes de obtener la lista.
```

#### Ejercicio 2 — Contar las tareas

**Objetivo:** agregar una operación que devuelva cuántas tareas tenemos.

**Dónde mirar:** métodos del controlador que atienden peticiones GET.

**Pista:** EF Core tiene `CountAsync()` para contar registros. Puedes pedirle al agente que te muestre cómo definir una nueva acción GET; revisa el código antes de aceptarlo.

**Cómo comprobarlo:** la cantidad debe aumentar al crear una tarea y disminuir al borrarla.

```scene
id: exercise-count
type: visual
visual: timeline
plain: true
items:
  - icon: 🔎
    label: Consulta nueva
    detail: ¿Cuántas tareas hay?
  - icon: 🔢
    label: EF Core
    detail: CountAsync()
  - icon: ✅
    label: Verificación
    detail: Crear una tarea debe aumentar el resultado
```

**Nota técnica solo para producción:** resultado esperado: un nuevo GET, por ejemplo `/api/todos/count`. Al construirlo, advertir que debe usar una ruta distinta a la consulta por identificador; ASP.NET Core resuelve las restricciones de ruta apropiadas si se declaran.

#### Ejercicio 3 — Admitir tareas canceladas

**Objetivo:** que una tarea también pueda tener el estado «Cancelada».

**Dónde mirar:** enum `Status`.

**Pista:** agrega el valor `Cancelled` al final de la lista de estados permitidos.

**Cómo comprobarlo:** crea una tarea con estado `Cancelled`, consúltala y comprueba que se conserva.

```scene
id: exercise-enum
type: code
language: csharp
file: src/back/TodoApi/Models/Status.cs
code: |-
  public enum Status
  {
      Pending,
      InProgress,
      Done
      // Agrega aquí la nueva opción.
  }
```

**Nota técnica solo para producción:** aquí no hace falta una migración: la base existente almacena el enum como entero y la API lo expone como texto mediante su configuración JSON.

```exercise
id: exercise-finish
type: checkpoint
prompt: Hice los tres cambios y comprobé que funcionan
explanation: "La idea no es memorizar todo C#: es empezar a reconocer el código, modificarlo y verificar el resultado."
```

**Cómo verificar durante la práctica (mostrar, no narrar como una lista de comandos):** reconstruir el contenedor después de cambiar el código, reiniciar el backend, probar cada operación desde Swagger y ejecutar las pruebas existentes. Los scripts del repositorio son `./run/build.sh`, `./run/restart.sh` y `./run/test.sh`; Swagger está disponible en `http://localhost:5080/swagger`.

### 15. Cierre: ya puedes seguir el recorrido

Cuando vuelvas a abrir este proyecto, ya tendrás una idea de lo que estás viendo. La API recibe peticiones; HTTP define cómo llegan; REST organiza las operaciones. Las clases describen las tareas, EF Core permite consultar y guardar sus datos y el controlador conecta todo. La inyección de dependencias proporciona las herramientas que necesita, y las migraciones permiten cambiar la base de datos a medida que evoluciona la aplicación.

No se trata de aprender todos los nombres de memoria. Se trata de poder leer una parte del código, entender para qué existe, hacer un cambio pequeño y comprobar que realmente funciona.

```scene
id: lesson-close
type: visual
visual: timeline
plain: true
items:
  - icon: 🌐
    label: Petición
    detail: Alguien pide una operación
  - icon: 🧭
    label: Controlador
    detail: Decide cómo atenderla
  - icon: 🧱
    label: Clases
    detail: Representan nuestros datos
  - icon: 💾
    label: EF Core y SQLite
    detail: Consultan y guardan
  - icon: ✅
    label: Verificación
    detail: Comprobamos el resultado
```
```exercise
id: finish
type: checkpoint
prompt: Terminé la lección 2
explanation: Ya puedes empezar a orientarte y hacer cambios sencillos en un backend real.
```
