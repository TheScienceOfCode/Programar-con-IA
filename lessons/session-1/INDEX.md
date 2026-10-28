---
title: "Lección 1: Tu primera aplicación con IA"
courseTitle: "Aprende a\nProgramar con IA"
language: es
objectives:
  - Preparar un editor y conectar un agente de programación
  - Construir y verificar una biblioteca web de videojuegos con ayuda de IA
  - Solicitar y comprobar un primer cambio en la aplicación
prerequisites:
  - Ninguno
---

# Lección 1 — Primer contacto con el computador para programar

**Proyecto:** Aprende a Programar con IA  
**Formato:** video guiado, una pantalla por parte, con su pregunta y botón Continuar  
**Público:** principiantes absolutos  
**Principio pedagógico:** primero construir algo útil; después aprender a entenderlo y dominarlo.

Este archivo es la única fuente de la lección. Cada `###` bajo **Partes** es una pantalla. Si trata un solo tema, el texto es la narración que se escucha, el bloque `scene` define lo que se ve y los bloques `exercise` son sus preguntas o prácticas. Si agrupa varios temas, cada `####` es una escena (con su texto y su `scene`) que se reproduce en el mismo video, y las preguntas quedan juntas al final de la pantalla.

## Partes

### 1. De una idea a una aplicación

Los computadores han ampliado nuestra capacidad de calcular, recordar y resolver problemas. Ahora la inteligencia artificial nos permite ir más allá: podemos describir una idea y trabajar con agentes capaces de escribir programas, encontrar errores y proponer soluciones. Incluso podemos tener varios agentes trabajando en diferentes tareas. No son infalibles, pero multiplican lo que podemos crear. Vamos a probarlo.

```scene
id: why-ai
type: visual
visual: timeline
items:
- icon: 🖥️
  label: Los computadores
  detail: calculan y recuerdan
- icon: ✍️
  label: Describes una idea
  detail: con tus palabras
- icon: 🤖
  label: Agentes de IA
  detail: escriben y corrigen
- icon: 🎮
  label: Aplicación terminada
  detail: tú la compruebas
```

```exercise
id: quiz-why-ai
type: multiple-choice
prompt: ¿Qué papel tiene la inteligencia artificial en este curso?
choices:
- Reemplaza por completo a la persona, que ya no debe revisar nada ni pensar.
- Trabaja como agentes que escriben y corrigen código, y tú diriges y validas.
- Sirve únicamente para buscar información en internet.
answer: 1
explanation: 'Los agentes multiplican lo que podemos crear, pero no son infalibles: siempre comprobamos
  el resultado.'
```

### 2. ¿Qué es un navegador?

Vamos a construir una aplicación web. Para eso, primero debemos saber qué es un navegador. Es el programa que nos permite acceder a internet y ver páginas, imágenes y videos. Y es muy importante, porque nos permite usar aplicaciones sin instalarlas en nuestra máquina: basta escribir una dirección y ya estamos dentro de una aplicación web.

```scene
id: browser-intro
type: visual
visual: browser-page
steps:
  - una-direccion.com
items:
  - icon: 📄
    label: Páginas
  - icon: 🖼️
    label: Imágenes
  - icon: 🎬
    label: Videos
  - icon: 🎮
    label: Aplicaciones web
```

```exercise
id: quiz-browser
type: multiple-choice
prompt: ¿Qué ventaja nos da usar una aplicación web en el navegador?
choices:
  - Entramos escribiendo una dirección, sin instalarla en el computador
  - Hay que instalarla antes en cada computador
  - Solo funciona si descargamos un archivo
answer: 0
explanation: Con solo escribir una dirección ya estamos dentro de la aplicación, sin instalar nada.
```

### 3. Descarga Visual Studio Code

Necesitamos un editor para trabajar con nuestros archivos y conversar con el agente. Usaremos Visual Studio Code; en Linux también puedes utilizar VSCodium. Entra a code punto visual studio punto com, barra download, y elige tu sistema: Windows, macOS o Linux.

```scene
id: download-editor
type: visual
visual: browser-download
items:
- icon: 🪟
  label: Windows
  detail: Instalador .exe
- icon: 🍎
  label: macOS
  detail: Archivo .zip
- icon: 🐧
  label: Linux
  detail: .deb · .rpm · VSCodium
```

```exercise
id: check-download
type: checkpoint
prompt: Ya descargué Visual Studio Code (o ya lo tenía)
explanation: ¡Listo! Sigue con la instalación.
```

### 4. Instálalo y ábrelo

Ahora instálalo. En Windows, abre el instalador y pulsa Siguiente hasta terminar. En macOS, abre el archivo descargado y arrastra Visual Studio Code a la carpeta Aplicaciones. En Linux, instala el paquete: con apt en Ubuntu y Debian, o con dnf en Fedora. Cuando termine, ábrelo. Si ya lo tienes, salta este paso.

```scene
id: install-editor
type: visual
visual: installer
items:
- icon: 🪟
  label: Windows
  steps:
  - Abre VSCodeUserSetup.exe
  - Acepta y pulsa Siguiente
  - Pulsa Instalar
  - Marca «Ejecutar» y Finalizar
- icon: 🍎
  label: macOS
  steps:
  - Abre el .zip descargado
  - Arrastra VS Code a Aplicaciones
  - Ábrelo desde Launchpad
  - Pulsa «Abrir» si macOS lo pide
- icon: 🐧
  label: Linux
  steps:
  - Descarga el .deb (Ubuntu/Debian) o el .rpm (Fedora)
  - 'Doble clic en el archivo: se abre «Instalar software»'
  - 'O por terminal, en la carpeta de descargas:'
  - $ sudo apt install ./archivo.deb
  - $ sudo dnf install ./archivo.rpm
  - Ábrelo desde el menú de aplicaciones
```

```exercise
id: check-install
type: checkpoint
prompt: Ya instalé y abrí Visual Studio Code
explanation: ¡Perfecto! Ahora instalaremos tu agente.
```

### 5. Instala tu agente

Abre el panel de extensiones, con el icono de cuadritos o con Control, Shift y X. Busca Claude Code o Codex y pulsa Instalar. Cuando termine, inicia sesión con tu cuenta.

```scene
id: install-extension
type: visual
visual: extensions
items:
- icon: 🟠
  label: Claude Code
  detail: Agente de programación de Anthropic
- icon: ⚫
  label: Codex
  detail: Agente de programación de OpenAI
```

```exercise
id: check-extension
type: checkpoint
prompt: Ya instalé la extensión e inicié sesión
explanation: ¡Bien! Falta abrir la carpeta de trabajo.
```

### 6. Abre una carpeta nueva

Ahora abre una carpeta de trabajo. En la pantalla de bienvenida pulsa Abrir carpeta. En la ventana que aparece, usa el botón Nueva carpeta, llámala mis-videojuegos y ábrela. Si el editor pregunta si confías en los autores, responde que sí. Ahí construiremos nuestra aplicación.

```scene
id: open-folder
type: visual
visual: open-folder
items:
- icon: 📂
  label: mis-videojuegos
```

```exercise
id: check-folder
type: checkpoint
prompt: Ya abrí la carpeta mis-videojuegos
explanation: ¡Excelente! Ahora abre el chat del agente.
```

### 7. Abre el chat del agente

Ahora abre el chat del agente. En Claude Code, pulsa su icono, arriba a la derecha del editor. En Codex, usa su icono en la barra lateral. Se abrirá un panel con una caja para escribirle: ahí pegaremos nuestro mensaje.

```scene
id: open-chat
type: visual
visual: open-chat
items:
- icon: 📂
  label: mis-videojuegos
```

```exercise
id: check-chat
type: checkpoint
prompt: Ya tengo abierto el chat del agente
explanation: ¡Listo para pedirle la aplicación!
```

### 8. Qué vamos a construir

#### Una biblioteca de videojuegos

Vamos a crear una biblioteca de videojuegos con portadas, búsqueda y favoritos. Tendremos usuarios normales y un administrador que podrá agregar, editar y eliminar juegos. También podremos cambiar de usuario con un clic.

```scene
id: game-library
type: visual
visual: app-preview
cards:
- label: Commander Keen 4
  detail: '1991'
  image: keen.jpg
- label: Another World
  detail: '1991'
  image: another-world.png
- label: Prince of Persia
  detail: '1989'
  image: prince-of-persia.jpg
- label: Prince of Persia 2
  detail: '1993'
  image: prince-of-persia-2.jpg
- label: Super Mario World
  detail: '1990'
  image: super-mario-world.png
- label: Simon the Sorcerer 2
  detail: '1995'
  image: simon-2.png
items:
- icon: 👤
  label: Usuario
- icon: 🛡️
  label: Administrador
```

```exercise
id: quiz-library
type: multiple-choice
prompt: En la biblioteca, ¿qué puede hacer el administrador que un usuario normal no puede?
choices:
- Agregar, editar y eliminar videojuegos
- Marcar favoritos
- Buscar juegos y cambiar de usuario
answer: 0
explanation: El usuario normal explora y guarda favoritos; solo el administrador gestiona el catálogo.
```

#### Frontend: lo que ves

Una aplicación web moderna tiene varios componentes. El frontend, o cliente, es lo que vemos directamente en el navegador: los botones y los formularios con los que interactuamos. Lo construiremos con React.

```scene
id: concept-frontend
type: visual
visual: frontend
cards:
- label: Commander Keen 4
  detail: '1991'
  image: keen.jpg
- label: Another World
  detail: '1991'
  image: another-world.png
- label: Prince of Persia
  detail: '1989'
  image: prince-of-persia.jpg
- label: Prince of Persia 2
  detail: '1993'
  image: prince-of-persia-2.jpg
items:
  - icon: 🔍
    label: Búsqueda
    detail: Escribes y filtras los juegos
  - icon: 🔘
    label: Botones
    detail: Agregar, favoritos, cambiar usuario
  - icon: 📝
    label: Formularios
    detail: Los datos que escribes
```

```exercise
id: quiz-frontend
type: multiple-choice
prompt: En una aplicación web, ¿qué es el frontend?
choices:
  - Lo que vemos y usamos en el navegador, como botones y formularios
  - El programa que guarda los datos
  - El contenedor que ejecuta la aplicación
answer: 0
explanation: El frontend, o cliente, es la parte que vemos y con la que interactuamos. Lo construiremos con React.
```

#### Backend: quien recibe las peticiones

El backend, o servidor, es el encargado de recibir las peticiones del navegador. Por ejemplo: muéstrame la información, modifícame este campo, guárdame esto, bórrame aquello. Recibe la petición, hace las validaciones y ejecuta las acciones. Usaremos ASP.NET Core.

```scene
id: concept-backend
type: visual
visual: backend
steps:
  - Muéstrame la información
  - Modifícame este campo
  - Guárdame esto
  - Bórrame aquello
items:
  - icon: 📥
    label: Recibe la petición
    detail: Llega desde el navegador
  - icon: 🛡️
    label: Hace validaciones
    detail: ¿Tienes permiso? ¿Los datos son correctos?
  - icon: ▶️
    label: Ejecuta la acción
    detail: Muestra, modifica, guarda o borra
```

```exercise
id: quiz-backend
type: multiple-choice
prompt: Pides «borra este juego» en el navegador. ¿Quién valida la petición y ejecuta la acción?
choices:
  - El frontend, que solo muestra los botones
  - El backend
  - Docker
answer: 1
explanation: El backend recibe la petición, hace las validaciones y ejecuta la acción.
```

```exercise
id: quiz-backend-validates
type: multiple-choice
prompt: Un usuario normal intenta eliminar un juego. ¿Qué debe hacer el backend?
choices:
- Ejecutarlo, porque el botón estaba visible
- Validar la petición y rechazarla, porque no tiene permiso
- Pedirle a Docker que lo decida
answer: 1
explanation: 'El backend siempre valida antes de ejecutar: no basta con ocultar el botón en el navegador.'
```

#### Base de datos: donde se guarda

La base de datos es donde el backend guarda la información de forma permanente; es decir, la persiste. Si marcamos un favorito, el backend lo escribe en la base de datos. Aunque apaguemos la aplicación, el dato sigue guardado; y al volver a encenderla, el backend lo lee y lo muestra. Usaremos SQLite.

```scene
id: concept-database
type: visual
visual: database
steps:
- Guardar|Marcas un favorito y el backend lo escribe en la base de datos
- Apagar|Apagas la aplicación, pero los datos siguen guardados en la base de datos
- 'Volver a abrir|La enciendes de nuevo: el backend lee la base de datos y el favorito sigue ahí'
items:
- label: Commander Keen 4
  icon: 🎮
  detail: '1991'
  image: keen.jpg
- label: Another World
  icon: 🎮
  detail: '1991'
  image: another-world.png
```

```exercise
id: quiz-database
type: multiple-choice
prompt: Apagas la aplicación y la vuelves a encender. ¿Por qué tus favoritos siguen ahí?
choices:
- Porque el backend los guardó en la base de datos, que los conserva aunque la aplicación esté apagada
- Porque el navegador los recuerda siempre
- Porque Docker los vuelve a crear al iniciar
answer: 0
explanation: Guardar de forma permanente se llama persistir. La base de datos conserva la información fuera de la aplicación.
```

#### Docker: la caja que lo contiene

Además usaremos Docker, que nos permite ejecutar la aplicación en contenedores, sin tener que instalar cosas directamente en nuestra máquina. Un contenedor reúne toda nuestra aplicación y sus dependencias, y funciona igual en cualquier computador, sin importar el sistema operativo. Así no tenemos que instalar nada y, además, podremos llevar la aplicación a cualquier lado.

```scene
id: concept-docker
type: visual
visual: docker
steps:
  - React · el frontend
  - ASP.NET Core · el backend
  - SQLite · los datos
  - Todas sus dependencias
items:
  - icon: 🪟
    label: Windows
  - icon: 🍎
    label: macOS
  - icon: 🐧
    label: Linux
```

```exercise
id: quiz-docker
type: multiple-choice
prompt: ¿Qué ventaja nos da Docker?
choices:
  - Ejecutar la aplicación sin instalar todo en el computador, y llevarla a cualquier lado
  - Hacer más bonitos los botones
  - Guardar los datos en la nube
answer: 0
explanation: El contenedor trae la aplicación y sus dependencias, y funciona igual en cualquier sistema operativo.
```

### 9. El prompt

#### ¿Qué es un prompt?

Ahora vamos a pedirle al agente que construya la aplicación. Lo haremos con un prompt: un mensaje en lenguaje natural que le enviamos al agente en el chat de VS Code. El agente lo interpreta y construye lo que describimos.

```scene
id: what-is-prompt
type: visual
visual: timeline
items:
- icon: ✍️
  label: Describes lo que quieres
  detail: en lenguaje natural
- icon: 📝
  label: El prompt
  detail: un mensaje de texto
- icon: 🤖
  label: El agente en VS Code
  detail: lo interpreta
- icon: 🎮
  label: Construye la aplicación
  detail: lo que describiste
```

```exercise
id: quiz-what-is-prompt
type: multiple-choice
prompt: ¿Qué es un prompt?
choices:
- Un programa que instalamos en el computador
- Un mensaje en lenguaje natural que le enviamos al agente para que lo interprete y construya lo que describimos
- Una carpeta donde el agente guarda los archivos
answer: 1
explanation: El prompt describe en lenguaje natural lo que queremos; el agente lo interpreta y lo construye.
```

#### Cómo está armado nuestro prompt

Revisa y lee el prompt, para que veas cómo se puede hacer. El prompt puede ser de muchas formas, tener más o menos detalle: depende de cada caso y de cuánto quieras dejar abierto para la IA. En nuestro caso vamos a definir qué queremos que construya la IA, con qué tecnologías y qué funcionalidades. Y, muy importante, le decimos a la IA misma cómo debe verificar que su trabajo realmente funciona: le pedimos que ejecute lo que construyó y que haga clics como un usuario real, para comprobar que la aplicación está correctamente implementada.

```scene
id: prompt-anatomy
type: visual
visual: prompt-anatomy
focus: 3
items:
- icon: 🎯
  label: Qué construir
  detail: Una biblioteca web de videojuegos
- icon: 🧰
  label: Con qué tecnologías
  detail: React, ASP.NET Core, SQLite y Docker Compose
- icon: ✅
  label: Qué funcionalidades
  detail: Catálogo, favoritos, cambio de usuario y administrador
- icon: 🔎
  label: Cómo verificar
  detail: Ejecuta la aplicación y haz clics como un usuario real
```

```exercise
id: quiz-validation
type: multiple-choice
prompt: ¿Por qué le pedimos a la IA que ejecute la aplicación y haga clics como un usuario real?
choices:
- Para que el prompt quede más corto
- Para que compruebe por sí misma que lo que construyó realmente funciona
- Para que la aplicación se vea más bonita
answer: 1
explanation: Código que parece correcto puede fallar al usarlo. Pedirle que lo ejecute y lo pruebe como un usuario real es la mejor forma de verificar que funciona.
```

```exercise
id: quiz-less-detail
type: multiple-choice
prompt: Si le damos al agente un prompt con menos detalle, ¿qué suele pasar?
choices:
- La IA decide por su cuenta lo que falta, y el resultado puede alejarse de lo que querías
- Siempre construye exactamente lo que imaginabas
- No puede construir nada
answer: 0
explanation: Menos detalle deja más decisiones abiertas a la IA. Puede servir para explorar, pero el resultado puede ser distinto a lo que esperabas.
```

```exercise
id: quiz-more-detail
type: multiple-choice
prompt: ¿Qué ganamos al dar más detalle en el prompt?
choices:
- Más control sobre el resultado, a cambio de dejar menos libertad a la IA
- Que la IA ya no necesite verificar su trabajo
- Que el prompt sea mejor en cualquier caso, sin importar lo que busquemos
answer: 0
explanation: Más detalle da más control, pero también te obliga a decidir más. Cuánto dejar abierto depende de cada caso.
```

### 10. Modelos y uso

#### Elige el modelo

El modelo es el cerebro que usa el agente, y no todos sirven para lo mismo. Uno más capaz, como Opus, o Sol si usas Codex, planifica y verifica mejor, pero es más lento y consume más de tu plan. Uno más ligero, como Sonnet, o Luna en Codex, responde rápido y gasta menos: ideal para ajustes pequeños. Para construir toda la aplicación, elige el más capaz; para retocarla, uno ligero. Cámbialo con el selector de modelo del chat.

```scene
id: choose-model
type: visual
visual: model-picker
focus: 0
items:
- icon: 🧠
  label: Opus · Sol en Codex
  detail: Más capaz, para tareas largas y complejas
  steps:
  - Planifica y verifica mejor
  - Más lento
  - Consume más del plan
- icon: ⚡
  label: Sonnet · Luna en Codex
  detail: Más ligero, para cambios pequeños
  steps:
  - Responde rápido
  - Gasta menos
```

```exercise
id: quiz-model-build
type: multiple-choice
prompt: Para construir la aplicación completa con nuestro prompt, ¿qué modelo conviene?
choices:
- Opus (Sol, si usas Codex), el más capaz
- Sonnet (Luna, si usas Codex), porque responde más rápido
- Da igual, todos dan el mismo resultado
answer: 0
explanation: Construir y verificar una aplicación completa es una tarea larga y compleja, y el modelo más capaz la maneja mejor.
```

```exercise
id: quiz-model-small
type: multiple-choice
prompt: Para cambiar un color de la aplicación, ¿qué modelo suele bastar?
choices:
- Sonnet (Luna, si usas Codex), más ligero y económico
- Solo Opus (Sol) sirve para hacer cambios
- Ninguno, los cambios se hacen a mano
answer: 0
explanation: Un cambio pequeño y claro no necesita el modelo más capaz. Uno ligero responde más rápido y gasta menos de tu plan.
```

```exercise
id: check-model
type: checkpoint
prompt: Ya elegí el modelo en el selector del chat
explanation: ¡Listo! Ahora veamos cuánto uso te queda.
```

#### Cuánto te queda del plan

Los planes tienen un límite de uso. En Claude Code, para ver cuánto te queda, abre la configuración en VS Code, entra a Account and usage y pulsa View details: verás el uso de la sesión de cinco horas y de la semana, y cuándo se reinician. También puedes escribir slash usage en el chat. En Codex, revisa el uso en tu cuenta de ChatGPT. Construye con el modelo capaz, pero vigila ese consumo.

```scene
id: plan-usage
type: visual
visual: usage-panel
steps:
- Abre la configuración de Claude Code
- Entra a Account & usage
- Pulsa View details
items:
- label: Session (5hr)
  detail: Se reinicia en 3 h
  value: 18
- label: Weekly (7 day)
  detail: Se reinicia en 4 días
  value: 42
```

```exercise
id: quiz-usage
type: multiple-choice
prompt: En Claude Code, ¿cómo ves cuánto te queda de tu plan?
choices:
- En Account & usage, con View details, o escribiendo /usage en el chat
- En la carpeta mis-videojuegos
- En el navegador, en localhost:3000
answer: 0
explanation: El panel Account & usage muestra el uso de la sesión de cinco horas y de la semana, y cuándo se reinician.
```

```exercise
id: check-usage
type: checkpoint
prompt: Ya revisé cuánto me queda de mi plan
explanation: ¡Bien! Ahora sí, a autorizar y enviar el prompt.
```

### 11. Autoriza, copia y envía

Lee la autorización: el prompt le pide al agente que instale programas en tu computador. Si estás de acuerdo, marca Acepto, copia el prompt, pégalo en el chat del agente en VS Code y envíalo.

```scene
id: authorize-prompt
type: visual
visual: prompt-flow
items:
- icon: ☑️
  label: 1. Acepto
- icon: 📋
  label: 2. Copiar el prompt
- icon: 💬
  label: 3. Pegarlo en el chat del agente y enviar
```

```exercise
id: authorize-and-copy
type: authorization
prompt: Permiso para instalar software
notice: Este mensaje autoriza al agente a instalar y configurar las herramientas necesarias para ejecutar
  el proyecto, incluido Docker. Estas operaciones pueden modificar la configuración de tu computador y
  requerir permisos de administrador o reiniciar el sistema.
consentLabel: Acepto y autorizo estas instalaciones y configuraciones para este proyecto.
buttonLabel: Copiar prompt completo
copyText: |-
  Quiero que construyas una biblioteca web de videojuegos. Soy principiante: haz el trabajo y explícame lo esencial con palabras sencillas.

  Tecnologías: React.js (frontend), ASP.NET Core con C# (backend), SQLite (datos) y Docker Compose para ejecutarlo.

  Funcionalidades:
  - Catálogo con portada, título, año, género, plataforma y descripción, con búsqueda y filtros.
  - Cuentas de demostración y botón Cambiar usuario para entrar con un clic.
  - Administrador: agregar, editar y eliminar videojuegos.
  - Usuario normal: explorar y marcar favoritos, sin editar el catálogo.
  - Validar los permisos también en el backend.
  - Conservar datos y favoritos al reiniciar.

  Diseño: inspirado en Steam, tonos azules oscuros, portadas y adaptación a pantallas pequeñas.

  Videojuegos iniciales:
  - Commander Keen 4: Secret of the Oracle (1991).
  - Another World (1991).
  - Prince of Persia (1989).
  - Prince of Persia 2: The Shadow and the Flame (1993).
  - Super Mario World (1990).
  - Simon the Sorcerer 2 (1995).

  Utiliza portadas reales de fuentes accesibles o imágenes de reemplazo.

  Instalación:
  Te autorizo a instalar y configurar las dependencias necesarias, incluido Docker y sus componentes.
  Detecta mi sistema operativo e instala lo que falte, sin limitarte a darme instrucciones. Si necesitas permisos de administrador o reiniciar, solicítame intervenir.
  No borres archivos personales ni realices cambios ajenos al proyecto.
  Trabaja en la carpeta actual, ejecuta la aplicación con Docker y dame la dirección para abrirla.

  Verificación:
  Antes de terminar, abre la aplicación en un navegador y comprueba que realmente funciona. Haz clic en los botones, cambia de usuario, agrega y edita videojuegos y prueba las funciones principales.
  Si algo falla, corrígelo y vuelve a comprobar. Si no puedes controlar el navegador, indícalo y guíame para verificar la aplicación.

  Al terminar, explícame brevemente qué construiste y cómo iniciar y detener la aplicación.

  Toma decisiones razonables sin preguntarme cada detalle. Las cuentas de demostración son solo para uso educativo local.
explanation: El prompt quedó copiado. Pégalo en el chat del agente; copiarlo no ejecuta ninguna instalación.
```

```exercise
id: quiz-authorize-prompt
type: multiple-choice
prompt: ¿Qué ocurre al copiar el prompt?
choices:
- Se instala todo automáticamente en ese momento
- 'No se ejecuta nada: el agente actúa solo cuando tú lo envías, y el sistema aún puede pedir permisos'
- El computador se reinicia
answer: 1
explanation: Copiar no ejecuta nada. Solo marcas «Acepto» si estás de acuerdo y luego envías el mensaje al agente.
```

```exercise
id: check-sent
type: checkpoint
prompt: Ya copié el prompt y se lo envié al agente
explanation: ¡Enviado! Veamos qué hace el agente.
```

### 12. El agente construye la aplicación

Al enviar el mensaje, el agente trabaja solo: detecta tu sistema, instala lo que falte, escribe el código, ejecuta la aplicación con Docker y la prueba en el navegador. Al final te da la dirección para abrirla. Puede tardar varios minutos y pedirte permisos. Léelos y acéptalos solo si estás de acuerdo.

```scene
id: agent-builds
type: visual
visual: agent-work
steps:
- Detecté tu sistema operativo
- Instalé Docker y sus componentes
- Escribí el backend y el frontend
- Ejecuté la aplicación con Docker
- La probé en el navegador
- 'Te di la dirección: http://localhost:3000'
```

```exercise
id: quiz-agent-builds
type: multiple-choice
prompt: Mientras el agente trabaja, ¿qué haces si te pide permisos?
choices:
- Los lees y aceptas solo si estás de acuerdo
- Los aceptas sin leer
- Cierras el editor
answer: 0
explanation: 'Puede pedir permisos para instalar o ejecutar cosas: léelos antes de aceptar.'
```

```exercise
id: check-built
type: checkpoint
prompt: El agente ya terminó de construir la aplicación
explanation: ¡Ya tienes una aplicación! Vamos a probarla.
```

### 13. Verifica la aplicación

Ya tenemos una aplicación, y el agente la dejó corriendo. Tú solo abre el navegador y escribe la dirección que te dio, por ejemplo localhost dos puntos tres mil. Ahora comprueba la aplicación: usa sus botones, cambia de usuario y prueba sus funciones. Si algo falla, díselo al agente para que lo corrija. Y si la aplicación no está corriendo, también se lo puedes pedir: dile que la ejecute y te dé la dirección.

```scene
id: verify-app
type: visual
visual: app-preview
cards:
- label: Commander Keen 4
  detail: '1991'
  image: keen.jpg
- label: Another World
  detail: '1991'
  image: another-world.png
- label: Prince of Persia
  detail: '1989'
  image: prince-of-persia.jpg
- label: Prince of Persia 2
  detail: '1993'
  image: prince-of-persia-2.jpg
- label: Super Mario World
  detail: '1990'
  image: super-mario-world.png
- label: Simon the Sorcerer 2
  detail: '1995'
  image: simon-2.png
items:
- icon: 👤
  label: Usuario
- icon: 🛡️
  label: Administrador
steps:
- Abre el navegador
- Escribe la dirección que te dio el agente
- Prueba los botones y cambia de usuario
- '💡 ¿No está corriendo? Díselo al agente: «Ejecuta la aplicación y dame la dirección»'
```

```exercise
id: quiz-verify-app
type: multiple-choice
prompt: ¿Quién ejecuta la aplicación?
choices:
- Tú, instalando cada herramienta a mano
- El agente la ejecuta y te da la dirección; tú solo abres el navegador
- Se ejecuta sola al copiar el prompt
answer: 1
explanation: Si no está corriendo, pídeselo al agente, por ejemplo «Ejecuta la aplicación y dame la dirección».
```

```exercise
id: check-opened
type: checkpoint
prompt: Ya abrí la aplicación en el navegador y la probé
explanation: ¡Muy bien! Ahora haremos un cambio.
```

### 14. Tu primer cambio

Ahora te toca a ti. Elige un cambio, pídeselo al agente y comprueba el resultado en el navegador.

```scene
id: first-change
type: visual
visual: choices
items:
- icon: 🌗
  label: Colores
  detail: Agrega un botón para cambiar entre tema claro y oscuro
- icon: ⭐
  label: Puntuación
  detail: Permite puntuar los videojuegos de una a cinco estrellas
- icon: 🔀
  label: Orden
  detail: Permite ordenar por título, año o género
```

```exercise
id: change-colors
type: prompt-copy
prompt: 'Opción 1: colores'
copyText: Agrega un botón para cambiar entre tema claro y oscuro y recuerda mi preferencia. Comprueba
  el cambio en el navegador y corrige cualquier problema que encuentres.
explanation: Instrucción copiada. Pégala en el chat del agente y comprueba ambos temas.
```

```exercise
id: change-rating
type: prompt-copy
prompt: 'Opción 2: puntuación'
copyText: Permite que cada usuario puntúe los videojuegos de una a cinco estrellas. Conserva las puntuaciones
  al reiniciar y comprueba el cambio en el navegador.
explanation: Instrucción copiada. Pégala en el chat del agente y prueba varias puntuaciones.
```

```exercise
id: change-order
type: prompt-copy
prompt: 'Opción 3: orden'
copyText: Permite ordenar los videojuegos por título, año o género. Comprueba cada opción en el navegador
  y corrige cualquier problema que encuentres.
explanation: Instrucción copiada. Pégala en el chat del agente y prueba los tres criterios.
```

```exercise
id: quiz-first-change
type: multiple-choice
prompt: ¿Cómo compruebas que tu primer cambio quedó bien?
choices:
- Confiando en que el agente no se equivoca
- Abriendo la aplicación en el navegador y probando el cambio
- Leyendo todo el código
answer: 1
explanation: Siempre se comprueba el resultado en el navegador.
```

```exercise
id: check-change
type: checkpoint
prompt: Ya le pedí un cambio al agente y lo comprobé en el navegador
explanation: ¡Lo lograste! Ya programaste con IA.
```

### 15. De una carpeta vacía a una aplicación

Empezamos con una carpeta vacía y terminamos con una aplicación que funciona. Todavía no entendemos todo su código. En las siguientes lecciones aprenderemos a comprenderlo y a tomar mejores decisiones al trabajar con inteligencia artificial.

```scene
id: closing
type: visual
visual: timeline
items:
- icon: 📂
  label: Carpeta vacía
- icon: 💬
  label: Un prompt
- icon: 🤖
  label: El agente construye
- icon: ✅
  label: Aplicación que funciona
```


## Notas del autor

- Las portadas de `assets/` son las carátulas oficiales de cada juego (de Wikipedia, uso ilustrativo). Se copian a la página al producir la lección.
- La portada de Commander Keen 4 es la de la colección «Goodbye, Galaxy!», que incluye ese episodio.

## Entregables de AutoTorial

- Lección audiovisual e interactiva con instrucciones para Windows, macOS y Linux.
- Autorización obligatoria antes de copiar el prompt.
- Tres ejercicios con instrucciones copiables.
- Publicación con `.autotorial/deploy-pages` y verificación de videos, interacciones y botones de copiar.
