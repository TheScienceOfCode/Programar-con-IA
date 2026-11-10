---
title: "Lección 4: Frontend en ReactJS"
courseTitle: "Aprende a\nProgramar con IA"
language: es
objectives:
  - Diferenciar C# y JavaScript, y saber dónde corre cada uno
  - Entender qué es el frontend y cómo se comunica con el backend
  - Construir interfaces con componentes, JSX y props
  - Usar estado, hooks, eventos y Context API en una aplicación real
  - Conectar React con la API mediante fetch y darle estilo con CSS
prerequisites:
  - Lección 3
  - Docker y un editor con agente de programación
---

# Lección 4 — Frontend en ReactJS

**Código:** https://github.com/TheScienceOfCode/Ejemplos-IA/tree/Todo-IA (carpeta `src/front`)

**Filosofía:** primero crear, después comprender. El estudiante pone en marcha el tablero y luego recorre su código.

**Formato:** una pantalla por cada `###`, con narración y escena visual. Las preguntas se hacen después de la narración.

**Criterio audiovisual:** lo que aparece entre el título de cada pantalla y `scene` es lo único que se narra. No narrar rutas de archivos ni fragmentos de código. Los fragmentos de las escenas de código son los del proyecto real (`src/front/src`); `// ...` marca líneas omitidas.

## Partes

### 1. ¿Qué es HTML?

Antes de programar el frontend, veamos de qué está hecha una página web. El navegador entiende HTML: un lenguaje para describir el contenido de una página con etiquetas. Cada etiqueta dice qué es cada cosa: h1 es un título, p es un párrafo, ul es una lista con sus elementos, y button es un botón. Las etiquetas se abren y se cierran, y unas van dentro de otras. A la derecha ves cómo lo dibuja el navegador. HTML solo describe el contenido: para darle estilo usaremos CSS, y para que responda a lo que hacemos, JavaScript.

```scene
id: que-es-html
type: visual
visual: jsx-preview
showResult: start
stepAt:
  - "El navegador entiende HTML"
  - "h1 es un título"
  - "p es un párrafo"
  - "ul es una lista con sus elementos"
  - "button es un botón"
  - "Las etiquetas se abren y se cierran"
  - "A la derecha ves cómo lo dibuja"
focusLines:
  - [1, 2, 3, 11, 12]
  - [4]
  - [5]
  - [6, 7, 8, 9]
  - [10]
  - [6, 9]
  - []
html: '<h1 style="margin:0 0 12px;font-size:38px">Mis tareas</h1><p style="margin:0 0 8px">Lo que tengo pendiente:</p><ul style="margin:0 0 18px;padding-left:34px"><li>Comprar café</li><li>Preparar la clase</li></ul><button style="font:inherit;font-size:22px;padding:6px 16px">Nueva tarea</button>'
code: |-
  <!DOCTYPE html>
  <html>
    <body>
      <h1>Mis tareas</h1>
      <p>Lo que tengo pendiente:</p>
      <ul>
        <li>Comprar café</li>
        <li>Preparar la clase</li>
      </ul>
      <button>Nueva tarea</button>
    </body>
  </html>
```

```exercise
id: html-quiz
type: multiple-choice
prompt: "¿Qué etiqueta de HTML usarías para un botón?"
choices:
  - "<button>"
  - "<h1>"
  - "<ul>"
answer: 0
explanation: "<button> es un botón, <h1> un título y <ul> una lista."
```

### 2. C# y JavaScript

Antes de empezar, una diferencia importante: el backend lo escribimos en C#, y el frontend lo vamos a escribir en JavaScript, el lenguaje que entienden los navegadores. Las ideas son las mismas: datos, funciones, listas y bloques de control. Pero se escriben distinto. En C# escribimos el tipo de cada dato, como int o string, y el compilador revisa el código antes de ejecutarlo. En JavaScript no escribimos los tipos: se descubren mientras el programa se ejecuta. Además, C# corre en el servidor, y JavaScript, en el navegador de cada persona. Y una pregunta para ti: ¿qué es un compilador? Investígalo con tu agente.

```scene
id: csharp-vs-js
type: code
language: csharp
split: 8
languages: [csharp, javascript]
focus:
  - lines: [1, 2, 3, 4, 5, 6, 7, 8]
    at: "el backend lo escribimos en C#"
  - lines: [9, 10, 11, 12, 13, 14, 15]
    at: "el frontend lo vamos a escribir en JavaScript"
  - lines: [2, 7]
    at: "En C# escribimos el tipo de cada dato"
  - lines: [10, 14]
    at: "En JavaScript no escribimos los tipos"
code: |2-
  // C#: escribimos el tipo de cada dato
  int Sumar(int a, int b)
  {
      return a + b;
  }

  var nombres = new List<string>();
  nombres.Add("Ana");
  // JavaScript: sin tipos
  function sumar(a, b) {
    return a + b;
  }

  const nombres = [];
  nombres.push("Ana");

```

```exercise
id: js-sumar-desde-hasta
type: code-completion
title: "Sumar desde a hasta b"
language: javascript
prompt: "El mismo ejercicio que hiciste en C#, ahora en JavaScript: completa sumarDesdeHasta(a, b) para que devuelva la suma de todos los números desde a hasta b, incluidos los dos. Usa un for."
starter: |-
  function sumarDesdeHasta(a, b) {
    let total = 0;
    // recorre desde a hasta b con un for
    // y suma cada número a total
    return total;
  }
solution: |-
  function sumarDesdeHasta(a, b) {
    let total = 0;
    for (let i = a; i <= b; i++) {
      total += i;
    }
    return total;
  }
tests:
  - name: "de 1 a 4 suma 10"
    expression: "sumarDesdeHasta(1, 4)"
    expected: 10
  - name: "de 3 a 5 suma 12"
    expression: "sumarDesdeHasta(3, 5)"
    expected: 12
  - name: "de 5 a 5 suma 5"
    expression: "sumarDesdeHasta(5, 5)"
    expected: 5
explanation: "Igual que en C#, pero sin tipos: let en lugar de int, y la función no declara qué devuelve."
```

```exercise
id: compilador-agente
type: prompt-copy
prompt: "¿Qué es un compilador? Pregúntaselo a tu agente"
buttonLabel: "Copiar pregunta"
copyText: "Explícame de forma sencilla, para alguien que está empezando a programar, qué es un compilador. Compara cómo se ejecuta un programa en C#, que se compila antes de ejecutarse, con uno en JavaScript, que el navegador ejecuta directamente. Usa un ejemplo corto de cada uno y dime qué ventajas tiene revisar el código antes de ejecutarlo."
explanation: "Pregunta copiada. Pégala en el chat de tu agente y lee su respuesta."
```

```exercise
id: csharp-vs-js-quiz
type: multiple-choice
prompt: "¿Cuál de estas líneas está escrita en JavaScript?"
choices:
  - "const nombres = [];"
  - "int edad = 30;"
  - "var nombres = new List<string>();"
answer: 0
explanation: "En JavaScript declaramos con const o let y no escribimos el tipo. int y List<string> son de C#."
```

### 3. ¿Qué es el frontend?

El frontend es la parte de la aplicación que vemos y usamos: botones, formularios y listas. Vive en el navegador. En la lección anterior construimos el backend, que guarda las tareas. Ahora vamos a construir su frontend: un tablero para ver las tareas, crearlas y moverlas. El frontend no guarda los datos por sí mismo: se los pide al backend. Veamos cómo, paso a paso. Primero, el frontend envía una petición HTTP pidiendo las tareas. El backend la recibe y consulta la base de datos. La base de datos le entrega las tareas guardadas. Entonces el backend responde con esas tareas en formato JSON: el texto con datos que conocimos en la lección anterior, con nombres y valores entre llaves. Por último, el frontend lee ese JSON y muestra cada tarea en pantalla.

```scene
id: que-es-frontend
type: visual
visual: request-flow
packets:
  - "GET /api/tareas"
  - "Consulta"
  - "Tareas"
  - "JSON"
steps:
  - "El frontend pide las tareas con una petición HTTP"
  - "El backend consulta la base de datos"
  - "La base de datos entrega las tareas"
  - "El backend responde con las tareas en JSON"
  - "El frontend lee el JSON y muestra las tareas"
stepAt:
  - "Primero, el frontend envía una petición HTTP"
  - "El backend la recibe"
  - "La base de datos le entrega"
  - "Entonces el backend responde"
  - "Por último, el frontend lee"
items:
  - icon: 🖥️
    label: Frontend
    detail: React, en el navegador
  - icon: ⚙️
    label: Backend
    detail: API en ASP.NET Core
  - icon: 💾
    label: Base de datos
    detail: SQLite
```

### 4. Primero, ponlo a funcionar

Primero vamos a crear, y después a comprender. Este es el tablero que vamos a tener: tres columnas, pendiente, en progreso y terminado, y cada tarea como un post-it. El código ya está en el proyecto de ejemplo. Pídele a tu agente que descargue la versión más reciente y la ejecute. Luego abre la aplicación en el navegador, crea una tarea y muévela entre las columnas.

```scene
id: tablero-real
type: visual
visual: screenshot
header: "http://localhost:5173"
items:
  - icon: 🗂️
    label: Tablero de tareas
    image: tablero.png
```

```exercise
id: front-ejecutar-prompt
type: prompt-copy
prompt: "Copia esta instrucción y pégala en el chat de tu agente"
buttonLabel: "Copiar instrucción"
copyText: "Descarga la versión más reciente de la rama Todo-IA del repositorio https://github.com/TheScienceOfCode/Ejemplos-IA (si ya lo tienes clonado, actualízalo con git pull). Construye y ejecuta el proyecto con ./run/build.sh y ./run/start.sh (usa Docker o, si no hay, Podman), ejecuta ./run/test.sh y dime la dirección del frontend para abrirlo en el navegador."
explanation: "Instrucción copiada. Pégala en el chat de tu agente y espera a que termine."
```

```exercise
id: front-ejecutar-check
type: checkpoint
prompt: "Abrí http://localhost:5173, creé una tarea y la moví entre las columnas"
explanation: "Ya tienes el tablero funcionando. Ahora veamos cómo está hecho."
```

### 5. ¿Qué es React?

```exercise
id: react-componentes-quiz
type: multiple-choice
prompt: "¿Qué es un componente de React?"
choices:
  - "Una pieza de la interfaz, como un post-it o una columna, que podemos reutilizar"
  - "Una tabla de la base de datos"
  - "Un endpoint del backend"
answer: 0
explanation: "La pantalla se arma juntando componentes pequeños: la página, el tablero, las columnas y los post-it."
```

#### ¿Qué es React?

React es una biblioteca de JavaScript: un conjunto de herramientas ya escritas para construir interfaces, es decir, lo que vemos y usamos en la pantalla. La creó Meta, la empresa de Facebook, y hoy la usan muchísimas aplicaciones web. Con React no le damos al navegador instrucciones paso a paso para cambiar la pantalla. Le describimos cómo debe verse según los datos y, cuando los datos cambian, React actualiza la pantalla por nosotros.

```scene
id: que-es-react
type: visual
visual: timeline
plain: true
items:
  - icon: 🧰
    label: Una biblioteca
    detail: Herramientas ya escritas
    at: "un conjunto de herramientas"
  - icon: 🌍
    label: Muy usada
    detail: Creada por Meta
    at: "La creó Meta"
  - icon: 📊
    label: Datos
    detail: Por ejemplo, las tareas
    at: "según los datos"
  - icon: 🖥️
    label: Pantalla
    detail: React la actualiza
    at: "React actualiza la pantalla"
```

#### ¿Qué es un componente?

En React, todo se arma con componentes. Un componente es una pieza de la pantalla con un nombre propio, como un botón, una tarjeta o una lista. Por dentro, es una función de JavaScript que devuelve lo que se ve. Los componentes se combinan: unos contienen a otros. Y se reutilizan: escribimos una pieza una vez y la usamos todas las veces que la necesitemos.

```scene
id: que-es-componente
type: visual
visual: timeline
plain: true
items:
  - icon: 🧩
    label: Una pieza de la pantalla
    detail: Con un nombre propio
    at: "Un componente es una pieza"
  - icon: ⚙️
    label: Una función
    detail: Devuelve lo que se ve
    at: "es una función de JavaScript"
  - icon: 📦
    label: Se combinan
    detail: Unos contienen a otros
    at: "Los componentes se combinan"
  - icon: ♻️
    label: Se reutilizan
    detail: Se escriben una vez
    at: "Y se reutilizan"
```

#### Los componentes del tablero

Veamos esa idea en nuestro tablero real. Toda la pantalla es un componente: la página de tareas. Dentro está el tablero, que reúne las tres columnas. Cada columna es otro componente, y contiene sus post-it. Cada post-it es un componente, y sus botones para mover la tarea, otro más. Unos componentes contienen a otros, como cajas dentro de cajas.

```scene
id: componentes-en-pantalla
type: visual
visual: annotated-screenshot
header: "http://localhost:5173"
cards:
  - icon: 🗂️
    label: Tablero de tareas
    image: estructura.png
items:
  - icon: 📄
    label: PaginaTareas
    area: [7.2, 1, 85.6, 98]
    value: 4
    at: "Toda la pantalla es un componente"
  - icon: 🗂️
    label: TableroTareas
    area: [7.8, 22.6, 84.4, 72.4]
    value: 1
    at: "Dentro está el tablero"
  - icon: 📚
    label: ColumnaTareas
    area: [8, 21.4, 27.6, 73]
    at: "Cada columna es otro componente"
  - icon: 📝
    label: TarjetaTarea
    area: [9, 33.6, 25.5, 30.4]
    value: 1
    at: "Cada post-it es un componente"
  - icon: 🔘
    label: AccionesTarjeta
    area: [9.9, 51.9, 23.7, 8.8]
    value: 2
    at: "sus botones para mover la tarea"
```

### 6. Un componente sencillo

Veamos un componente sencillo, fuera del proyecto. Saludo es una función que recibe un nombre y devuelve un título. Lo que devuelve parece HTML, pero es JavaScript: se llama JSX, y entre llaves ponemos el nombre. Para usar el componente, lo escribimos como una etiqueta y le pasamos el nombre. Si lo usamos dos veces, con nombres distintos, React dibuja dos saludos en la pantalla.

```scene
id: componente-sencillo
type: visual
visual: jsx-preview
stepAt:
  - "Saludo es una función"
  - "entre llaves ponemos el nombre"
  - "lo escribimos como una etiqueta"
  - "Si lo usamos dos veces"
  - "React dibuja dos saludos"
focusLines:
  - [1, 2, 3]
  - [2]
  - [8]
  - [8, 9]
  - [8, 9]
html: '<h2 style="margin:0 0 14px">Hola, Ana</h2><h2 style="margin:0">Hola, Luis</h2>'
code: |-
  function Saludo({ nombre }) {
    return <h2>Hola, {nombre}</h2>;
  }

  function App() {
    return (
      <div>
        <Saludo nombre="Ana" />
        <Saludo nombre="Luis" />
      </div>
    );
  }
```

```exercise
id: playground-saludo
type: playground
title: "Edita el saludo"
prompt: "Edita el componente y mira el resultado a la derecha. Primero haz que Saludo muestre Hola, antes del nombre. Luego agrega un tercer Saludo con tu nombre."
starter: |-
  function Saludo({ nombre }) {
    return <p>{nombre}</p>;
  }

  function App() {
    return (
      <div>
        <Saludo nombre="Ana" />
        <Saludo nombre="Luis" />
      </div>
    );
  }
solution: |-
  function Saludo({ nombre }) {
    return <p>Hola, {nombre}</p>;
  }

  function App() {
    return (
      <div>
        <Saludo nombre="Ana" />
        <Saludo nombre="Luis" />
        <Saludo nombre="Sofía" />
      </div>
    );
  }
checks:
  - name: "cada saludo dice Hola, y el nombre"
    expression: "document.querySelectorAll('p').length > 0 && [...document.querySelectorAll('p')].every((p) => /^Hola, \\S/.test(p.textContent))"
    expected: true
  - name: "hay al menos tres saludos"
    expression: "document.querySelectorAll('p').length >= 3"
    expected: true
explanation: "Cambiaste el componente una sola vez y todos los saludos se actualizaron: así se reutiliza un componente."
```

```exercise
id: playground-etiquetas
type: playground
title: "Llena la lista"
prompt: "El componente y la línea que pinta las columnas ya están listos. Solo llena la lista para que se vea: Sonic con 100 disponibles, Zelda con 400 y Doom con 50."
starter: |-
  function EtiquetaColumna({ titulo, cantidad }) {
    return <p>{titulo} <span>disponibles: {cantidad}</span></p>;
  }

  function App() {
    const columnas = [
      { titulo: '', cantidad: 0 },
      { titulo: '', cantidad: 0 },
      { titulo: '', cantidad: 0 },
    ];
    return (
      <div>
        {/* Esto es un comentario, no afecta la ejecución */ }
        {/* Con este ejemplo, pintamos todo el contenido del arreglo de columnas, pasando respectivos titulo y cantidad al componente. */ }
        {columnas.map((columna) => (
          <EtiquetaColumna
            /*Cuando tenemos una lista en JSX es buena práctica definir un key, de forma que React identifique de forma inequívoca el elemento */
            key={columna.titulo}
            titulo={columna.titulo}
            cantidad={columna.cantidad}
          />
        ))}
      </div>
    );
  }
solution: |-
  function EtiquetaColumna({ titulo, cantidad }) {
    return <p>{titulo} <span>disponibles: {cantidad}</span></p>;
  }

  function App() {
    const columnas = [
      { titulo: 'Sonic', cantidad: 100 },
      { titulo: 'Zelda', cantidad: 400 },
      { titulo: 'Doom', cantidad: 50 },
    ];
    return (
      <div>
        {/* Esto es un comentario, no afecta la ejecución */ }
        {/* Con este ejemplo, pintamos todo el contenido del arreglo de columnas, pasando respectivos titulo y cantidad al componente. */ }
        {columnas.map((columna) => (
          <EtiquetaColumna
            /*Cuando tenemos una lista en JSX es buena práctica definir un key, de forma que React identifique de forma inequívoca el elemento */
            key={columna.titulo}
            titulo={columna.titulo}
            cantidad={columna.cantidad}
          />
        ))}
      </div>
    );
  }
checks:
  - name: "hay una etiqueta por cada elemento de la lista"
    expression: "document.querySelectorAll('p').length"
    expected: 3
  - name: "cada etiqueta muestra su título y su cantidad"
    expression: "[...document.querySelectorAll('p')].map((h) => h.textContent.replace(/\\s+/g, ' ').trim())"
    expected: ["Sonic disponibles: 100", "Zelda disponibles: 400", "Doom disponibles: 50"]
explanation: "Cambiaste solo los datos y la pantalla se actualizó: el mismo componente se pinta una vez por cada elemento de la lista, con sus props. En la parte de map lo veremos con calma."
```

### 7. Estado: un saludo que cambia

```exercise
id: playground-saludo-estado
type: playground
title: "Cuenta las letras"
prompt: "Escribe tu nombre en el campo y mira cómo cambia el saludo. Luego completa el segundo párrafo para que diga: Tu nombre tiene N letras. Pista: el texto tiene una propiedad length con su cantidad de letras."
starter: |-
  function Saludo() {
    const [nombre, setNombre] = useState('');
    return (
      <div>
        <input
          value={nombre}
          onChange={(event) => setNombre(event.target.value)}
          placeholder="Escribe tu nombre"
        />
        <p>Hola, {nombre}</p>
        <p>{/*Tu nombre tiene {X} letras*/}</p>
      </div>
    );
  }

  function App() {
    return <Saludo />;
  }
solution: |-
  function Saludo() {
    const [nombre, setNombre] = useState('');
    return (
      <div>
        <input
          value={nombre}
          onChange={(event) => setNombre(event.target.value)}
          placeholder="Escribe tu nombre"
        />
        <p>Hola, {nombre}</p>
        <p>Tu nombre tiene {nombre.length} letras</p>
      </div>
    );
  }

  function App() {
    return <Saludo />;
  }
checks:
  - name: "al escribir Ana, saluda y cuenta 3 letras"
    expression: "(async () => { await escribir('Ana'); return [...document.querySelectorAll('p')].map((p) => p.textContent.replace(/\\s+/g, ' ').trim()); })()"
    expected: ["Hola, Ana", "Tu nombre tiene 3 letras"]
  - name: "al escribir Sofía, cuenta 5 letras"
    expression: "(async () => { await escribir('Sofía'); return [...document.querySelectorAll('p')].map((p) => p.textContent.replace(/\\s+/g, ' ').trim()); })()"
    expected: ["Hola, Sofía", "Tu nombre tiene 5 letras"]
explanation: "Cada letra que escribes cambia el estado, y React vuelve a dibujar los dos párrafos con el valor nuevo."
```

Hasta ahora, nuestro saludo siempre muestra lo mismo. ¿Y si queremos que cambie mientras escribimos? Para eso los componentes tienen estado: la memoria de un componente. Con useState creamos un valor, nombre, que empieza vacío, y una función para cambiarlo, setNombre. El campo de texto muestra el valor de nombre. Cada vez que escribimos, el evento onChange llama a setNombre con el texto nuevo. React vuelve a dibujar el componente, y el saludo cambia al instante. A esto se le llama un campo controlado: React guarda lo que escribimos en el estado.

```scene
id: saludo-estado
type: visual
visual: jsx-preview
showResult: start
stepAt:
  - "los componentes tienen estado"
  - "Con useState creamos un valor"
  - "El campo de texto muestra"
  - "el evento onChange llama a setNombre"
  - "el saludo cambia al instante"
  - "un campo controlado"
focusLines:
  - [2]
  - [2]
  - [5, 6, 8]
  - [7]
  - [9]
  - [5, 6, 7, 8]
notes:
  - "estado"
  - "useState"
  - ""
  - "evento"
  - ""
  - "campo controlado"
html: '<input value="Ana" style="font:inherit;font-size:24px;padding:6px 12px;margin-bottom:14px;width:80%"><p style="margin:0">Hola, Ana</p>'
code: |2-
  function Saludo() {
    const [nombre, setNombre] = useState('');
    return (
      <div>
        <input
          value={nombre}
          onChange={(event) => setNombre(event.target.value)}
        />
        <p>Hola, {nombre}</p>
      </div>
    );
  }
```

### 8. Estado y hooks

```exercise
id: playground-contador
type: playground
title: "Un contador con useState"
prompt: "Este contador usa useState. Haz click en Sumar para probarlo. Luego agrega un botón Reiniciar que vuelva el contador a 0."
starter: |-
  function Contador() {
    const [clicks, setClicks] = useState(0);
    return (
      <div>
        <p>Hiciste {clicks} clicks</p>
        <button onClick={() => setClicks(clicks + 1)}>Sumar</button>
      </div>
    );
  }

  function App() {
    return <Contador />;
  }
solution: |-
  function Contador() {
    const [clicks, setClicks] = useState(0);
    return (
      <div>
        <p>Hiciste {clicks} clicks</p>
        <button onClick={() => setClicks(clicks + 1)}>Sumar</button>
        <button onClick={() => setClicks(0)}>Reiniciar</button>
      </div>
    );
  }

  function App() {
    return <Contador />;
  }
checks:
  - name: "Sumar cuenta los clicks"
    expression: "(async () => { await clic('Sumar'); await clic('Sumar'); return document.querySelector('p').textContent; })()"
    expected: "Hiciste 2 clicks"
  - name: "Reiniciar vuelve a 0"
    expression: "(async () => { await clic('Sumar'); await clic('Reiniciar'); return document.querySelector('p').textContent; })()"
    expected: "Hiciste 0 clicks"
explanation: "Cada click llama a setClicks, el estado cambia y React vuelve a dibujar el componente con el número nuevo."
```

```exercise
id: hooks-quiz
type: multiple-choice
prompt: "¿Para qué usa la página de tareas useEffect?"
choices:
  - "Para cargar las tareas del backend cuando la página aparece"
  - "Para cambiar el color de los post-it"
  - "Para guardar el título que escribimos en el formulario"
answer: 0
explanation: "useEffect ejecuta algo cuando el componente aparece en pantalla. Guardar lo que escribimos es trabajo de useState."
```

#### useState: recordar un valor

Ya vimos que useState le da memoria a un componente: un valor y una función para cambiarlo. En el ejemplo lo usamos para recordar lo que escribimos. El título empieza vacío. El campo muestra ese valor y, cada vez que escribimos, llamamos a la función que lo cambia. React vuelve a dibujar el componente con el valor nuevo.

```scene
id: hook-usestate
type: code
language: jsx
focus:
  - lines: [1]
    at: "Ya vimos que useState"
  - lines: [1]
    at: "El título empieza vacío"
  - lines: [3, 4]
    at: "El campo muestra ese valor"
  - lines: [5]
    at: "cada vez que escribimos"
code: |2-
  const [titulo, setTitulo] = useState('');

  <input
    value={titulo}
    onChange={(event) => setTitulo(event.target.value)}
    required
    autoFocus
  />
```

#### useEffect: hacer algo al aparecer

Otro hook muy usado es useEffect. Sirve para hacer algo cuando el componente aparece en pantalla. Nuestra página lo usa para cargar las tareas del backend apenas se muestra. La lista vacía del final indica que solo debe hacerlo una vez. La página también usa useState, para recordar si el popup de nueva tarea está abierto.

```scene
id: hook-useeffect
type: code
language: jsx
focus:
  - lines: [6, 7, 8]
    at: "Otro hook muy usado es useEffect"
  - lines: [7]
    at: "para cargar las tareas"
  - lines: [8]
    at: "La lista vacía del final"
  - lines: [3]
    at: "para recordar si el popup"
code: |2-
  export default function PaginaTareas() {
    const { tareas, cargandoTareas, error, cargarTareas } = useTareasAcciones();
    const [creando, setCreando] = useState(false);

    // Al mostrarse la página por primera vez, carga las tareas del backend.
    useEffect(() => {
      cargarTareas();
    }, []);
    // ...
  }
```

### 9. Eventos e interacciones

```exercise
id: js-titulo-valido
type: code-completion
title: "Validar el título"
language: javascript
prompt: "Antes de crear una tarea conviene revisar el título. Completa tituloValido(titulo): debe devolver true si tiene al menos 3 caracteres sin contar los espacios del principio y del final."
starter: |-
  function tituloValido(titulo) {
    // pista: titulo.trim() quita los espacios del principio y del final
    return false;
  }
solution: |-
  function tituloValido(titulo) {
    return titulo.trim().length >= 3;
  }
tests:
  - name: "un título vacío no es válido"
    expression: "tituloValido('')"
    expected: false
  - name: "solo espacios y dos letras no es válido"
    expression: "tituloValido('   ab   ')"
    expected: false
  - name: "un título normal es válido"
    expression: "tituloValido('Comprar café')"
    expected: true
explanation: "trim quita los espacios de los extremos y length cuenta los caracteres. Con esto podrías desactivar el botón Crear tarea mientras el título no sea válido."
```

```exercise
id: eventos-siguiente
type: code-completion
title: "El estado siguiente"
language: javascript
prompt: "Los botones del post-it necesitan saber cuál es el estado siguiente. Completa siguienteEstado(estado): debe devolver el estado que sigue en la lista, o null si ya es el último."
starter: |-
  const ESTADOS = ['Pendiente', 'EnProgreso', 'Terminada'];

  function siguienteEstado(estado) {
    // busca la posición del estado en ESTADOS
    // y devuelve el que sigue, o null si es el último
    return null;
  }
solution: |-
  const ESTADOS = ['Pendiente', 'EnProgreso', 'Terminada'];

  function siguienteEstado(estado) {
    const posicion = ESTADOS.indexOf(estado);
    return posicion >= 0 && posicion < ESTADOS.length - 1 ? ESTADOS[posicion + 1] : null;
  }
tests:
  - name: "después de Pendiente viene EnProgreso"
    expression: "siguienteEstado('Pendiente')"
    expected: "EnProgreso"
  - name: "después de EnProgreso viene Terminada"
    expression: "siguienteEstado('EnProgreso')"
    expected: "Terminada"
  - name: "Terminada es el último"
    expression: "siguienteEstado('Terminada')"
    expected: null
explanation: "indexOf da la posición del estado en la lista; el siguiente está en la posición + 1. El proyecto hace lo mismo en estados.js."
```

#### Clicks

Los eventos son las cosas que hace el usuario: un click, escribir, enviar un formulario. En React los atendemos con funciones. Cuando hacemos click en el botón de un post-it, se ejecuta mover. Ahí le pedimos al contexto, que veremos más adelante, que mueva la tarea. Mientras tanto, el botón queda desactivado; y si algo falla, mostramos un mensaje. Este componente maneja interacciones: además de mostrar, responde a lo que hace el usuario.

```scene
id: evento-click
type: code
language: jsx
split: 12
focus:
  - lines: [13, 14, 15, 16, 17, 18, 19]
    at: "Cuando hacemos click"
  - lines: [1, 16]
    at: "se ejecuta mover"
  - lines: [5]
    at: "le pedimos al contexto"
  - lines: [2, 15]
    at: "el botón queda desactivado"
  - lines: [7]
    at: "si algo falla"
code: |2-
  async function mover(estado) {
    setMoviendo(true);
    setError('');
    try {
      await moverTarea(id, estado.id);
    } catch {
      setError('No se pudo mover la tarea.');
    } finally {
      setMoviendo(false);
    }
  }

  <button
    className="boton boton-pequeno"
    disabled={moviendo}
    onClick={() => mover(siguiente)}
  >
    {siguiente.nombre} →
  </button>
```

#### Formularios

Con los formularios pasa algo parecido. Al enviar el formulario, se ejecuta handleSubmit. Primero evitamos que el navegador recargue la página, que es lo que haría por defecto. Luego creamos la tarea con el título y la descripción que guardamos en el estado, y cerramos el popup. Si algo falla, mostramos un error y dejamos el formulario abierto.

```scene
id: evento-formulario
type: code
language: jsx
split: 13
focus:
  - lines: [14, 15, 16]
    at: "Al enviar el formulario"
  - lines: [1]
    at: "se ejecuta handleSubmit"
  - lines: [2]
    at: "Primero evitamos"
  - lines: [6]
    at: "Luego creamos la tarea"
  - lines: [7]
    at: "cerramos el popup"
  - lines: [9, 10]
    at: "Si algo falla"
code: |2-
  async function handleSubmit(event) {
    event.preventDefault();
    setGuardando(true);
    setError('');
    try {
      await crearTarea(titulo, descripcion);
      onCerrar();
    } catch {
      setError('No se pudo crear la tarea.');
      setGuardando(false);
    }
  }

  <form
    className="modal"
    onSubmit={handleSubmit}
    // ...
```

### 10. Así se organiza el proyecto

Ahora abramos el proyecto en el editor. El frontend tiene una carpeta por cada tipo de pieza: las llamadas al backend, los componentes, el contexto, las páginas y los estilos. El punto de entrada es App: envuelve la página de tareas con el proveedor de datos, que veremos más adelante. Los componentes viven en su propia carpeta, un archivo por componente. Abrimos esa carpeta y elegimos el post-it, TarjetaTarea, para ver cómo está hecho.

```scene
id: front-vscode
type: visual
visual: vscode
header: front
focus: 11
openAt: "elegimos el post-it"
openFocus: 7
stepAt:
  - "una carpeta por cada tipo de pieza"
  - "El punto de entrada es App"
  - "envuelve la página de tareas"
items:
  - icon: 📁
    label: src
    value: 0
  - icon: 📁
    label: api
    value: 1
  - icon: 📂
    label: components
    value: 1
  - icon: 📄
    label: AccionesTarjeta.jsx
    value: 2
    at: "Abrimos esa carpeta"
  - icon: 📄
    label: ColumnaTareas.jsx
    value: 2
    at: "Abrimos esa carpeta"
  - icon: 📄
    label: ModalNuevaTarea.jsx
    value: 2
    at: "Abrimos esa carpeta"
  - icon: 📄
    label: TableroTareas.jsx
    value: 2
    at: "Abrimos esa carpeta"
  - icon: 📄
    label: TarjetaTarea.jsx
    value: 2
    at: "Abrimos esa carpeta"
  - icon: 📁
    label: context
    value: 1
  - icon: 📁
    label: pages
    value: 1
  - icon: 📁
    label: styles
    value: 1
  - icon: 📄
    label: App.jsx
    value: 1
  - icon: 📄
    label: estados.js
    value: 1
  - icon: 📄
    label: main.jsx
    value: 1
code: |2-
  import { TareasProvider } from './context/TareasContext.jsx';
  import PaginaTareas from './pages/PaginaTareas.jsx';

  export default function App() {
    return (
      <TareasProvider>
        <PaginaTareas />
      </TareasProvider>
    );
  }
openCode: |2-
  import { useTareaPorId } from '../context/TareasContext.jsx';
  import AccionesTarjeta from './AccionesTarjeta.jsx';

  // Un post-it: recibe solo el id y obtiene la tarea del contexto.
  export default function TarjetaTarea({ id }) {
    const tarea = useTareaPorId(id);
    return (
      <article className={`tarjeta tarjeta-${tarea.estado}`}>
        <h3 className="tarjeta-titulo">{tarea.titulo}</h3>
        {tarea.descripcion && (
          <p className="tarjeta-descripcion">{tarea.descripcion}</p>
        )}
        <AccionesTarjeta id={id} />
      </article>
    );
  }
```

### 11. Un componente real: el post-it

Este es el post-it por dentro, y a la derecha, cómo se ve en el navegador. Recibe solo el identificador de la tarea. Con él obtiene la tarea del contexto, usando un hook propio que veremos más adelante. Luego devuelve lo que se ve: el título, la descripción si la tiene y, al final, otro componente con los botones.

```scene
id: componente-tarjeta
type: visual
visual: jsx-preview
showResult: start
cards:
  - icon: 📝
    label: Post-it
    image: tarjeta-comprar.png
stepAt:
  - "Recibe solo el identificador"
  - "obtiene la tarea del contexto"
  - "el título"
  - "la descripción si la tiene"
  - "otro componente con los botones"
focusLines:
  - [1]
  - [2]
  - [5]
  - [6, 7, 8]
  - [9]
notes:
  - "props"
  - "hook"
  - ""
  - ""
  - "otro componente"
code: |2-
  export default function TarjetaTarea({ id }) {
    const tarea = useTareaPorId(id);
    return (
      <article className={`tarjeta tarjeta-${tarea.estado}`}>
        <h3 className="tarjeta-titulo">{tarea.titulo}</h3>
        {tarea.descripcion && (
          <p className="tarjeta-descripcion">{tarea.descripcion}</p>
        )}
        <AccionesTarjeta id={id} />
      </article>
    );
  }
```

### 12. Un componente más complejo

#### Lo que vamos a ver

Ahora veamos un componente más completo: AccionesTarjeta, los botones del post-it. En pocas líneas junta varias ideas: hooks, estado, renderizado condicional y eventos. Ya conoces el estado y los eventos; aquí los vemos trabajando juntos, y sumamos dos ideas nuevas: un hook propio y el renderizado condicional.

```scene
id: complejo-intro
type: visual
visual: timeline
plain: true
items:
  - icon: 🪝
    label: Hooks
    detail: Funciones especiales de React
    at: "hooks"
  - icon: 🧠
    label: Estado
    detail: La memoria del componente
    at: "estado"
  - icon: 🔀
    label: Renderizado condicional
    detail: Mostrar algo solo si...
    at: "renderizado condicional"
  - icon: 👆
    label: Eventos
    detail: Responder a un click
    at: "y eventos"
```

#### Hooks

Primero, los hooks. Un hook es una función especial de React que le da a un componente una capacidad extra: recordar algo, o tomar datos del contexto. Se reconocen fácil: su nombre empieza con use, y se llaman al principio del componente. Aquí hay varios. useTareaPorId le pide al contexto la tarea de este post-it, a partir de su id. useTareasAcciones trae las acciones compartidas, como mover una tarea. Y useState sirve para que el componente recuerde un valor: lo vemos a continuación.

```scene
id: complejo-hooks
type: code
language: jsx
focus:
  - lines: [2, 3, 4, 5]
    at: "Un hook es una función especial"
  - lines: [2, 3, 4, 5]
    at: "su nombre empieza con use"
  - lines: [2]
    at: "useTareaPorId le pide al contexto"
  - lines: [3]
    at: "useTareasAcciones trae las acciones"
  - lines: [4, 5]
    at: "Y useState"
code: |2-
  export default function AccionesTarjeta({ id }) {
    const tarea = useTareaPorId(id);
    const { moverTarea } = useTareasAcciones();
    const [moviendo, setMoviendo] = useState(false);
    const [error, setError] = useState('');
    // ...
  }
```

#### Estado con useState

El estado es la memoria de un componente. useState nos da dos cosas: el valor actual y una función para cambiarlo. moviendo empieza en falso: al principio no estamos moviendo nada. error empieza vacío: todavía no hay errores. Cuando pulsamos un botón, se ejecuta mover, que primero llama a setMoviendo con verdadero. Luego intenta mover la tarea. Para eso usamos try, que intenta algo; catch, que atrapa el error si algo falla; y finally, que se ejecuta siempre. Si algo falla, guardamos un mensaje con setError. Y al terminar, pase lo que pase, volvemos moviendo a falso. Cada vez que cambiamos el estado, React vuelve a dibujar el componente.

```scene
id: complejo-estado
type: code
language: jsx
focus:
  - lines: [1, 2]
    at: "El estado es la memoria"
  - lines: [1]
    at: "moviendo empieza en falso"
  - lines: [2]
    at: "error empieza vacío"
  - lines: [5]
    at: "llama a setMoviendo con verdadero"
  - lines: [7, 8, 9, 10, 11, 12, 13]
    at: "Para eso usamos try"
  - lines: [10]
    at: "guardamos un mensaje con setError"
  - lines: [12]
    at: "volvemos moviendo a falso"
  - lines: [1, 2]
    at: "Cada vez que cambiamos el estado"
code: |2-
  const [moviendo, setMoviendo] = useState(false);
  const [error, setError] = useState('');

  async function mover(estado) {
    setMoviendo(true);
    setError('');
    try {
      await moverTarea(id, estado.id);
    } catch {
      setError('No se pudo mover la tarea.');
    } finally {
      setMoviendo(false);
    }
  }
```

#### Renderizado condicional

Con el estado de la tarea calculamos el estado anterior y el siguiente: una tarea pendiente no tiene anterior, y una terminada no tiene siguiente. Ahora viene el renderizado condicional: mostrar algo solo si se cumple una condición. Los dos signos que ves después de anterior significan: si hay un estado anterior, dibuja este botón; si no, no dibujes nada. Lo mismo con el botón siguiente, y con el mensaje de error: solo aparece si hay un error. Por eso una tarea en progreso, como la de la derecha, muestra dos botones.

```scene
id: complejo-condicional
type: visual
visual: jsx-preview
showResult: start
cards:
  - icon: 📝
    label: Post-it en progreso
    image: tarjeta-preparar.png
stepAt:
  - "calculamos el estado anterior y el siguiente"
  - "renderizado condicional"
  - "si hay un estado anterior"
  - "Lo mismo con el botón siguiente"
  - "con el mensaje de error"
  - "Por eso una tarea en progreso"
focusLines:
  - [1, 2]
  - [4, 5, 6, 7, 8, 9, 10]
  - [4, 5, 6]
  - [7, 8, 9]
  - [10]
  - [4, 5, 6, 7, 8, 9]
code: |2-
  const anterior = estadoAnterior(tarea.estado);
  const siguiente = estadoSiguiente(tarea.estado);

  {anterior && (
    // botón ← para retroceder
  )}
  {siguiente && (
    // botón → para avanzar
  )}
  {error && <p className="tarjeta-error">{error}</p>}
```

#### Eventos: el botón

Por último, los eventos: lo que pasa cuando el usuario hace algo, como un click. Cada botón tiene varias partes. className le da estilo con CSS. disabled lo desactiva mientras moviendo sea verdadero, para no pulsarlo dos veces. onClick dice qué hacer al hacer click: llamar a mover con el estado siguiente. Y entre las etiquetas va el texto del botón: el nombre del estado y una flecha. El botón para retroceder es igual, con la flecha al otro lado.

```scene
id: complejo-boton
type: visual
visual: jsx-preview
showResult: start
cards:
  - icon: 🔘
    label: Botones
    image: botones-preparar.png
stepAt:
  - "Cada botón tiene varias partes"
  - "className le da estilo"
  - "disabled lo desactiva"
  - "onClick dice qué hacer"
  - "entre las etiquetas va el texto"
focusLines:
  - [2, 3, 4, 5, 6, 7, 8]
  - [3]
  - [4]
  - [5]
  - [7]
code: |2-
  {siguiente && (
    <button
      className="boton boton-pequeno"
      disabled={moviendo}
      onClick={() => mover(siguiente)}
    >
      {siguiente.nombre} →
    </button>
  )}
```

### 13. Pausa: practica JavaScript

Hagamos una pausa para practicar JavaScript. El texto de cada botón es el nombre del estado con una flecha: a la izquierda si retrocede, y a la derecha si avanza. Escribe una función que arme ese texto. Y otra que, a partir del estado que guarda el backend, devuelva el nombre que vemos en pantalla.

```scene
id: pausa-ejemplos
type: code
language: javascript
focus:
  - lines: [1, 2]
    at: "El texto de cada botón"
  - lines: [2]
    at: "a la izquierda si retrocede"
  - lines: [1]
    at: "a la derecha si avanza"
  - lines: [4, 5, 6]
    at: "devuelva el nombre que vemos"
code: |2-
  etiquetaBoton('Terminado', 'siguiente');  // 'Terminado →'
  etiquetaBoton('Pendiente', 'anterior');   // '← Pendiente'

  nombreDeEstado('Pendiente');   // 'Pendiente'
  nombreDeEstado('EnProgreso');  // 'En progreso'
  nombreDeEstado('Terminada');   // 'Terminado'
```

```exercise
id: js-etiqueta-boton
type: code-completion
title: "El texto del botón"
language: javascript
prompt: "Completa etiquetaBoton(nombre, direccion): si la dirección es 'anterior', la flecha va a la izquierda (← Pendiente); si no, a la derecha (Terminado →)."
starter: |-
  function etiquetaBoton(nombre, direccion) {
    // usa un if para decidir dónde va la flecha
    return nombre;
  }
solution: |-
  function etiquetaBoton(nombre, direccion) {
    if (direccion === 'anterior') {
      return `← ${nombre}`;
    }
    return `${nombre} →`;
  }
tests:
  - name: "avanzar pone la flecha a la derecha"
    expression: "etiquetaBoton('Terminado', 'siguiente')"
    expected: "Terminado →"
  - name: "retroceder pone la flecha a la izquierda"
    expression: "etiquetaBoton('Pendiente', 'anterior')"
    expected: "← Pendiente"
explanation: "Con un if elegimos qué texto devolver. En JavaScript comparamos con ===, que revisa que el valor y el tipo sean iguales."
```

```exercise
id: js-nombre-estado
type: code-completion
title: "El nombre del estado"
language: javascript
prompt: "Completa nombreDeEstado(estado): 'EnProgreso' se muestra como En progreso, 'Terminada' como Terminado, y 'Pendiente' como Pendiente."
starter: |-
  function nombreDeEstado(estado) {
    // usa if / else if para elegir el nombre
    return estado;
  }
solution: |-
  function nombreDeEstado(estado) {
    if (estado === 'EnProgreso') {
      return 'En progreso';
    } else if (estado === 'Terminada') {
      return 'Terminado';
    }
    return 'Pendiente';
  }
tests:
  - name: "Pendiente"
    expression: "nombreDeEstado('Pendiente')"
    expected: "Pendiente"
  - name: "En progreso"
    expression: "nombreDeEstado('EnProgreso')"
    expected: "En progreso"
  - name: "Terminado"
    expression: "nombreDeEstado('Terminada')"
    expected: "Terminado"
explanation: "El backend guarda EnProgreso o Terminada; en pantalla mostramos un nombre más amable. El proyecto guarda esos nombres en estados.js."
```

### 14. Props, map y filter

```exercise
id: js-titulos
type: code-completion
title: "Practica map"
language: javascript
prompt: "Practica map: completa titulosDe(tareas) para que devuelva una lista con el título de cada tarea."
starter: |-
  function titulosDe(tareas) {
    // pista: tareas.map((tarea) => ...)
    return [];
  }
solution: |-
  function titulosDe(tareas) {
    return tareas.map((tarea) => tarea.titulo);
  }
tests:
  - name: "devuelve los títulos en orden"
    expression: "titulosDe([{ id: 1, titulo: 'Comprar café' }, { id: 2, titulo: 'Preparar la clase' }])"
    expected: ["Comprar café", "Preparar la clase"]
  - name: "sin tareas devuelve una lista vacía"
    expression: "titulosDe([])"
    expected: []
explanation: "map transforma cada elemento de la lista en otro valor. En la columna, cada tarea se transforma en un post-it."
```

```exercise
id: props-filtrar
type: code-completion
title: "Practica filter"
language: javascript
prompt: "Practica filter: completa tareasDeEstado(tareas, estado) para que devuelva solo las tareas de ese estado."
starter: |-
  function tareasDeEstado(tareas, estado) {
    // pista: tareas.filter((tarea) => ...)
    return [];
  }
solution: |-
  function tareasDeEstado(tareas, estado) {
    return tareas.filter((tarea) => tarea.estado === estado);
  }
tests:
  - name: "devuelve las pendientes"
    expression: "tareasDeEstado([{ id: 1, estado: 'Pendiente' }, { id: 2, estado: 'Terminada' }, { id: 3, estado: 'Pendiente' }], 'Pendiente').map((t) => t.id)"
    expected: [1, 3]
  - name: "devuelve las terminadas"
    expression: "tareasDeEstado([{ id: 1, estado: 'Pendiente' }, { id: 2, estado: 'Terminada' }], 'Terminada').map((t) => t.id)"
    expected: [2]
  - name: "sin tareas de ese estado devuelve una lista vacía"
    expression: "tareasDeEstado([{ id: 1, estado: 'Pendiente' }], 'EnProgreso').length"
    expected: 0
explanation: "filter se queda solo con los elementos que cumplen la condición. Es lo mismo que hace el tablero antes de pasarle las tareas a cada columna."
```

#### Props: los datos que recibe

¿De dónde saca el post-it su identificador? Lo recibe de la columna, mediante props. Las props son los datos que un componente le pasa a otro, como los parámetros de una función. La columna recibe su título y su lista de tareas, y muestra cuántas hay. Para dibujar un post-it por cada tarea usa map: map recorre la lista y transforma cada tarea en un componente, al que le pasa su id como prop.

```scene
id: props-columna
type: code
language: jsx
focus:
  - lines: [11]
    at: "Lo recibe de la columna"
  - lines: [3]
    at: "La columna recibe su título"
  - lines: [7]
    at: "muestra cuántas hay"
  - lines: [10, 11, 12]
    at: "usa map"
  - lines: [11]
    at: "le pasa su id como prop"
code: |2-
  import TarjetaTarea from './TarjetaTarea.jsx';

  export default function ColumnaTareas({ titulo, tareas }) {
    return (
      <section className="columna">
        <h2 className="columna-titulo">
          {titulo} <span className="columna-cantidad">{tareas.length}</span>
        </h2>
        {tareas.length === 0 && <p className="columna-vacia">Sin tareas</p>}
        {tareas.map((tarea) => (
          <TarjetaTarea key={tarea.id} id={tarea.id} />
        ))}
      </section>
    );
  }
```

#### filter: las tareas de cada columna

¿Y cómo recibe cada columna solo sus tareas? El tablero recorre los estados y crea una columna por cada uno. A cada columna le pasa la lista filtrada con filter: filter recorre la lista y se queda solo con las tareas que cumplen una condición; aquí, que su estado sea el de la columna.

```scene
id: filter-tablero
type: code
language: jsx
focus:
  - lines: [8]
    at: "El tablero recorre los estados"
  - lines: [9, 10, 11, 12, 13]
    at: "crea una columna por cada uno"
  - lines: [12]
    at: "con filter"
  - lines: [12]
    at: "que su estado sea el de la columna"
code: |2-
  import { ESTADOS } from '../estados.js';
  import ColumnaTareas from './ColumnaTareas.jsx';

  // Muestra una columna por estado, cada una con sus tareas.
  export default function TableroTareas({ tareas }) {
    return (
      <div className="tablero">
        {ESTADOS.map((estado) => (
          <ColumnaTareas
            key={estado.id}
            titulo={estado.nombre}
            tareas={tareas.filter((tarea) => tarea.estado === estado.id)}
          />
        ))}
      </div>
    );
  }
```

### 15. Compartir datos con Context API

```exercise
id: js-cambiar-estado
type: code-completion
title: "Copiar con un estado nuevo"
language: javascript
prompt: "moverTarea crea una copia de la tarea con el estado nuevo: { ...tarea, estado }. Completa cambiarEstado(tarea, estado) para que devuelva una copia con el estado cambiado, sin modificar la tarea original."
starter: |-
  function cambiarEstado(tarea, estado) {
    // pista: los tres puntos (...) copian todas las propiedades de un objeto
    return tarea;
  }
solution: |-
  function cambiarEstado(tarea, estado) {
    return { ...tarea, estado };
  }
tests:
  - name: "la copia tiene el estado nuevo"
    expression: "cambiarEstado({ id: 1, titulo: 'Comprar café', estado: 'Pendiente' }, 'Terminada').estado"
    expected: "Terminada"
  - name: "la copia conserva las demás propiedades"
    expression: "cambiarEstado({ id: 1, titulo: 'Comprar café', estado: 'Pendiente' }, 'Terminada').titulo"
    expected: "Comprar café"
  - name: "la tarea original no cambia"
    expression: "(() => { const tarea = { id: 1, estado: 'Pendiente' }; cambiarEstado(tarea, 'Terminada'); return tarea.estado; })()"
    expected: "Pendiente"
explanation: "En React no modificamos los datos directamente: creamos una copia con el cambio, y así React sabe que algo cambió y vuelve a dibujar."
```

```exercise
id: context-indexar
type: code-completion
title: "Indexar por id"
language: javascript
prompt: "El contexto guarda las tareas en un objeto indexado por id. Completa indexarPorId(lista) para que convierta una lista de tareas en un objeto como { 1: {...}, 2: {...} }."
starter: |-
  function indexarPorId(lista) {
    const porId = {};
    // por cada tarea de la lista, guárdala en porId usando su id
    return porId;
  }
solution: |-
  function indexarPorId(lista) {
    const porId = {};
    for (const tarea of lista) {
      porId[tarea.id] = tarea;
    }
    return porId;
  }
tests:
  - name: "encuentra cada tarea por su id"
    expression: "indexarPorId([{ id: 1, titulo: 'Comprar café' }, { id: 2, titulo: 'Preparar la clase' }])[2].titulo"
    expected: "Preparar la clase"
  - name: "guarda todas las tareas"
    expression: "Object.keys(indexarPorId([{ id: 1 }, { id: 5 }, { id: 9 }])).length"
    expected: 3
  - name: "una lista vacía da un objeto vacío"
    expression: "Object.keys(indexarPorId([])).length"
    expected: 0
explanation: "Con un objeto indexado por id, encontrar o reemplazar una tarea es directo: tareas[id]. Es lo que hace cargarTareas en el contexto."
```

#### Un solo lugar para las tareas

Varios componentes necesitan las mismas tareas: la página las carga, cada post-it busca su tarea, los botones las mueven y el formulario crea tareas nuevas. Podríamos pasarlas de prop en prop por todos los componentes, pero sería incómodo. Con Context API las guardamos en un solo lugar, el proveedor de tareas, y cualquier componente puede usarlas.

```scene
id: context-hub
type: visual
visual: hub
items:
  - icon: 🧠
    label: TareasContext
    detail: tareas y operaciones
    at: "en un solo lugar"
  - icon: 📄
    label: PaginaTareas
    detail: cargarTareas()
    at: "la página las carga"
  - icon: 🗂️
    label: TarjetaTarea
    detail: useTareaPorId()
    at: "cada post-it busca su tarea"
  - icon: 🔘
    label: AccionesTarjeta
    detail: moverTarea()
    at: "los botones las mueven"
  - icon: ➕
    label: ModalNuevaTarea
    detail: crearTarea()
    at: "el formulario crea tareas nuevas"
```

#### El proveedor de tareas

Así se crea el contexto. El proveedor guarda en su estado las tareas, si se están cargando y si hubo un error. Las tareas se guardan en un objeto indexado por su identificador, para encontrar cada una rápidamente.

```scene
id: context-provider
type: code
language: jsx
focus:
  - lines: [1]
    at: "Así se crea el contexto"
  - lines: [4, 5, 6]
    at: "guarda en su estado"
  - lines: [4]
    at: "un objeto indexado por su identificador"
code: |2-
  const TareasContext = createContext(null);

  export function TareasProvider({ children }) {
    const [tareas, setTareas] = useState({});
    const [cargandoTareas, setCargandoTareas] = useState(false);
    const [error, setError] = useState('');
    // ... cargarTareas, cargarTarea, crearTarea y moverTarea
  }
```

#### Compartir el valor

Luego el proveedor reúne los datos y las operaciones en un valor, y lo comparte con todos los componentes que envuelve. Cualquier componente que llame a useTareasAcciones recibe ese valor, y puede leer las tareas o ejecutar una operación.

```scene
id: context-value
type: code
language: jsx
split: 10
focus:
  - lines: [1, 2, 3, 4, 5, 6, 7, 8, 9]
    at: "reúne los datos y las operaciones"
  - lines: [11, 12, 13, 14, 15]
    at: "lo comparte con todos los componentes"
  - lines: [18, 19, 20]
    at: "llame a useTareasAcciones"
code: |2-
    const value = {
      tareas,
      cargandoTareas,
      error,
      cargarTareas,
      cargarTarea,
      crearTarea,
      moverTarea,
    };

    return (
      <TareasContext.Provider value={value}>
        {children}
      </TareasContext.Provider>
    );
  }

  export function useTareasAcciones() {
    return useContext(TareasContext);
  }
```

#### Un hook propio: useTareaPorId

¿Recuerdas el hook que usaba el post-it? Es un hook propio, hecho con otros hooks. useTareasAcciones devuelve todo lo que comparte el contexto. useTareaPorId toma de ahí las tareas y devuelve solo la del identificador que le pedimos. Así, el post-it no necesita recibir toda la tarea: le basta su id. Por convención, los nombres de los hooks empiezan con use.

```scene
id: context-hook
type: code
language: jsx
focus:
  - lines: [6]
    at: "Es un hook propio"
  - lines: [1, 2, 3]
    at: "useTareasAcciones devuelve todo"
  - lines: [7]
    at: "toma de ahí las tareas"
  - lines: [8]
    at: "devuelve solo la del identificador"
  - lines: [1, 6]
    at: "empiezan con use"
code: |2-
  export function useTareasAcciones() {
    return useContext(TareasContext);
  }

  // Hook propio: devuelve una sola tarea a partir de su id.
  export function useTareaPorId(id) {
    const { tareas } = useTareasAcciones();
    return tareas[id];
  }
```

#### Actualizar solo una tarea

Mover una tarea es una operación compartida. Primero enviamos al backend una copia de la tarea con su nuevo estado: los tres puntos copian todas sus propiedades. Después volvemos a consultar solo esa tarea, y reemplazamos únicamente esa entrada en el objeto de tareas. El resto queda igual, y React solo actualiza el post-it que cambió.

```scene
id: context-movertarea
type: code
language: jsx
focus:
  - lines: [6, 7, 8, 9]
    at: "Mover una tarea"
  - lines: [7]
    at: "Primero enviamos al backend"
  - lines: [7]
    at: "los tres puntos copian"
  - lines: [8]
    at: "Después volvemos a consultar"
  - lines: [3, 4]
    at: "reemplazamos únicamente esa entrada"
code: |2-
  // Vuelve a consultar una sola tarea y actualiza solo esa en el estado.
  async function cargarTarea(id) {
    const tarea = await api.obtenerTarea(id);
    setTareas((anteriores) => ({ ...anteriores, [id]: tarea }));
  }

  async function moverTarea(id, estado) {
    await api.actualizarTarea({ ...tareas[id], estado });
    await cargarTarea(id);
  }
```

### 16. Comunicación con el backend

```exercise
id: fetch-quiz
type: multiple-choice
prompt: "¿Qué método HTTP usa el frontend para mover una tarea a otra columna?"
choices:
  - "PUT, enviando la tarea con su nuevo estado"
  - "GET, porque solo consulta"
  - "DELETE, porque la quita de la columna"
answer: 0
explanation: "Mover es actualizar: el frontend envía la tarea completa con el estado nuevo usando PUT, igual que en Swagger."
```

#### fetch: pedir datos al backend

Todas las llamadas al backend están en un solo archivo. Usamos fetch, la función del navegador para hacer peticiones HTTP, con las mismas direcciones que probamos en Swagger. Si el servidor responde con un error, lanzamos una excepción para mostrar un mensaje. Si responde bien, convertimos el JSON de la respuesta en objetos de JavaScript.

```scene
id: api-fetch
type: code
language: javascript
focus:
  - lines: [1, 2]
    at: "Todas las llamadas al backend"
  - lines: [5]
    at: "Usamos fetch"
  - lines: [6, 7, 8]
    at: "Si el servidor responde con un error"
  - lines: [10]
    at: "convertimos el JSON"
code: |2-
  // Todas las llamadas HTTP al backend están en este archivo.
  const URL_TAREAS = '/api/tareas';

  async function pedir(url, opciones) {
    const respuesta = await fetch(url, opciones);
    if (!respuesta.ok) {
      throw new Error(`El servidor respondió ${respuesta.status}`);
    }
    // 204 No Content: el servidor no devuelve datos
    return respuesta.status === 204 ? null : respuesta.json();
  }
```

#### Enviar datos

Para crear una tarea usamos el método POST. Le decimos al servidor que enviamos JSON, y convertimos la tarea a JSON para mandarla en el cuerpo de la petición. Las demás operaciones siguen el mismo patrón.

```scene
id: api-post
type: code
language: javascript
focus:
  - lines: [3]
    at: "usamos el método POST"
  - lines: [4]
    at: "enviamos JSON"
  - lines: [5]
    at: "convertimos la tarea a JSON"
code: |2-
  export function crearTarea(tarea) {
    return pedir(URL_TAREAS, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(tarea),
    });
  }
```

### 17. CSS y estilos

```exercise
id: css-cambiar
type: checkpoint
prompt: "Cambié el color principal y el de los post-it en las variables, reconstruí con ./run/build.sh y ./run/start.sh, y vi el cambio en el navegador"
explanation: "Con las variables cambiaste la apariencia de toda la aplicación tocando un solo archivo."
```

#### Variables

Los estilos están en archivos CSS tradicionales. Al principio definimos variables: valores con nombre, como colores, bordes, sombras y el color de los post-it en cada columna. El resto de los estilos usa esas variables en lugar de repetir los valores. Si cambiamos el color principal en un solo lugar, cambian todos los botones que lo usan.

```scene
id: css-variables
type: code
language: css
split: 12
focus:
  - lines: [1, 19]
    at: "Al principio definimos variables"
  - lines: [2, 3, 4, 5, 6]
    at: "colores, bordes, sombras"
  - lines: [14, 15, 16]
    at: "el color de los post-it"
  - lines: [6]
    at: "Si cambiamos el color principal"
code: |2-
  :root {
    --bg: #f4f1ea;
    --surface: #ffffff;
    --text: #2b2b2b;
    --muted: #6b6b6b;
    --primary: #2563eb;
    --primary-text: #ffffff;
    --danger: #c0392b;
    --border: #e2ddd2;
    --radius: 8px;
    --shadow: 0 2px 6px rgba(0, 0, 0, 0.12);

    /* Color de los post-it en cada columna */
    --note-pendiente: #fff3a3;
    --note-progreso: #cfe8ff;
    --note-terminada: #d4f5d0;

    --font: system-ui, sans-serif;
  }
```

#### Clases reutilizables

Una clase agrupa estilos con un nombre. Todos los post-it usan la clase tarjeta, que usa las variables para el color, el borde y la sombra. Las otras dos clases se aplican además, según el estado de la tarea, y solo cambian el color. En el componente, el nombre de la clase se arma con el estado: así cada columna tiene su color sin repetir el resto. Prueba tú: cambia el color principal y el de los post-it, reconstruye la aplicación y mira el resultado.

```scene
id: css-clases
type: code
language: css
focus:
  - lines: [1, 2, 3, 4, 5, 6, 7]
    at: "Una clase agrupa estilos"
  - lines: [2, 3, 4]
    at: "usa las variables"
  - lines: [9, 10, 11, 13, 14, 15]
    at: "Las otras dos clases"
  - lines: [10, 14]
    at: "solo cambian el color"
code: |2-
  .tarjeta {
    background: var(--note-pendiente);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    padding: 14px;
    margin-bottom: 12px;
  }

  .tarjeta-EnProgreso {
    background: var(--note-progreso);
  }

  .tarjeta-Terminada {
    background: var(--note-terminada);
  }
```

### 18. Recorrido completo

Repasemos el recorrido completo. El usuario hace click en el botón de un post-it. React ejecuta la acción del contexto, que hace una petición HTTP al backend. El backend actualiza la tarea en la base de datos y responde. Entonces cambia el estado compartido, y la interfaz se actualiza sola: el post-it aparece en su nueva columna.

```scene
id: recorrido-completo
type: visual
visual: timeline
plain: true
items:
  - icon: 👆
    label: Click
    detail: El usuario pulsa un botón
    at: "El usuario hace click"
  - icon: ⚛️
    label: React
    detail: moverTarea()
    at: "React ejecuta la acción"
  - icon: 📤
    label: Petición HTTP
    detail: PUT /api/tareas/{id}
    at: "hace una petición HTTP"
  - icon: ⚙️
    label: Backend
    detail: Guarda y responde
    at: "El backend actualiza la tarea"
  - icon: 🧠
    label: Estado
    detail: Cambia esa tarea
    at: "cambia el estado compartido"
  - icon: 🖥️
    label: Interfaz
    detail: Se actualiza sola
    at: "la interfaz se actualiza sola"
```

```exercise
id: js-contar-por-estado
type: code-completion
title: "Contar por estado"
language: javascript
prompt: "Cada columna muestra cuántas tareas tiene. Completa contarPorEstado(tareas) para que devuelva cuántas tareas hay en cada estado."
starter: |-
  function contarPorEstado(tareas) {
    const cuenta = { Pendiente: 0, EnProgreso: 0, Terminada: 0 };
    // recorre las tareas y suma 1 al estado de cada una
    return cuenta;
  }
solution: |-
  function contarPorEstado(tareas) {
    const cuenta = { Pendiente: 0, EnProgreso: 0, Terminada: 0 };
    for (const tarea of tareas) {
      cuenta[tarea.estado] += 1;
    }
    return cuenta;
  }
tests:
  - name: "cuenta las tareas de cada estado"
    expression: "contarPorEstado([{ estado: 'Pendiente' }, { estado: 'Pendiente' }, { estado: 'Terminada' }])"
    expected: {"Pendiente": 2, "EnProgreso": 0, "Terminada": 1}
  - name: "sin tareas, todo en cero"
    expression: "contarPorEstado([])"
    expected: {"Pendiente": 0, "EnProgreso": 0, "Terminada": 0}
explanation: "Con for...of recorremos la lista, y con cuenta[tarea.estado] usamos el estado como nombre de la propiedad que sumamos."
```

```exercise
id: recorrido-quiz
type: multiple-choice
prompt: "Después de que el backend responde, ¿qué hace que el post-it aparezca en su nueva columna?"
choices:
  - "Que cambia el estado compartido y React vuelve a dibujar la interfaz"
  - "Que el navegador recarga la página completa"
  - "Que el backend dibuja la pantalla"
answer: 0
explanation: "El frontend no recarga la página: actualiza el estado y React redibuja solo lo que cambió."
```

### 19. Ejercicio final: responsables de tareas

```exercise
id: responsables-guia
type: prompt-copy
prompt: "Si te atascas, pide a tu agente que te guíe (sin hacerlo por ti)"
buttonLabel: "Copiar instrucción"
copyText: "Estoy haciendo un ejercicio: agregar responsables a las tareas del proyecto Todo-IA (backend en src/back/TareaApi y frontend React en src/front). Quiero hacerlo yo mismo para aprender, así que no escribas la solución completa: guíame paso a paso, explícame qué archivo tocar en cada paso y por qué, y revisa el código que yo escriba. Empecemos por el modelo Responsable y la migración."
explanation: "Instrucción copiada. Pégala en el chat de tu agente y avanza paso a paso."
```

```exercise
id: responsables-api
type: checkpoint
prompt: "En Swagger puedo crear, consultar y editar responsables, y asignar un responsableId a una tarea"
explanation: "El backend está listo: modelo, relación, migración y endpoints."
```

```exercise
id: responsables-ui
type: checkpoint
prompt: "En el tablero puedo agregar y editar responsables, y elegir el responsable de una tarea en un selector"
explanation: "Usaste componentes, estado, formularios y fetch para una función nueva."
```

```exercise
id: responsables-postit
type: checkpoint
prompt: "Cada post-it muestra el nombre de su responsable, y al recargar la página sigue ahí"
explanation: "¡Lo lograste! El dato viaja de la base de datos al post-it y se conserva."
```

#### El reto

Ahora te toca a ti. Vamos a agregar responsables a las tareas. Primero, en el backend: crea una entidad Responsable, con un identificador y un nombre, y endpoints para consultar, crear y editar responsables. Luego, una relación opcional entre la tarea y su responsable, con un campo responsableId. Si hiciste el reto de la lección anterior, ya tienes esta parte.

```scene
id: responsables-modelo
type: visual
visual: table-relation
steps:
  - "Una tarea puede tener un responsable"
stepAt:
  - "una relación opcional"
items:
  - icon: 👤
    label: Responsable
    at: "crea una entidad Responsable"
    steps:
      - "Id (PK)"
      - "Nombre"
  - icon: 📋
    label: Tarea
    at: "entre la tarea y su responsable"
    steps:
      - "Id (PK)"
      - "Titulo"
      - "Descripcion"
      - "Estado"
      - "ResponsableId (FK)"
```

#### En el frontend

Después, en el frontend: una pantalla o un popup para agregar y editar responsables; un selector con los responsables disponibles, para asignar o cambiar el de cada tarea; y el nombre del responsable dentro del post-it. Usa lo que aprendiste: componentes pequeños, estado con useState, formularios controlados, fetch para hablar con el backend y el contexto para compartir los datos. Para saber que quedó funcionando, revisa tres cosas: que puedes manejar responsables desde Swagger, que puedes asignarlos desde el tablero, y que el nombre sigue en el post-it al recargar la página.

```scene
id: responsables-front
type: visual
visual: timeline
plain: true
items:
  - icon: ✏️
    label: Responsables
    detail: Agregar y editar
    at: "para agregar y editar responsables"
  - icon: 🔽
    label: Selector
    detail: Asignar o cambiar
    at: "un selector con los responsables"
  - icon: 📝
    label: Post-it
    detail: Muestra el nombre
    at: "el nombre del responsable dentro del post-it"
  - icon: ✅
    label: Verifica
    detail: Swagger, tablero y recarga
    at: "Para saber que quedó funcionando"
```

