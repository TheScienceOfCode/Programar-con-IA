---
title: "Lección 1: Primer contacto con el computador para programar"
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

Este archivo es la única fuente de la lección. Cada `###` bajo **Partes** es una pantalla: el texto es la narración que se escucha, el bloque `scene` define lo que se ve y los bloques `exercise` son sus preguntas o prácticas.

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
- Reemplaza por completo a la persona, que ya no debe revisar nada
- Trabaja como agente que escribe y corrige programas, y tú compruebas el resultado
- Sirve únicamente para buscar información en internet
answer: 1
explanation: 'Los agentes multiplican lo que podemos crear, pero no son infalibles: siempre comprobamos
  el resultado.'
```

### 2. Descarga Visual Studio Code

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


### 3. Instálalo y ábrelo

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


### 4. Instala tu agente

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


### 5. Abre una carpeta nueva

Ahora abre una carpeta de trabajo. En la pantalla de bienvenida pulsa Abrir carpeta. En la ventana que aparece, usa el botón Nueva carpeta, llámala mis-videojuegos y ábrela. Si el editor pregunta si confías en los autores, responde que sí. Ahí construiremos nuestra aplicación.

```scene
id: open-folder
type: visual
visual: open-folder
items:
- icon: 📂
  label: mis-videojuegos
```


### 6. Abre el chat del agente

Ahora abre el chat del agente. En Claude Code, pulsa su icono, arriba a la derecha del editor. En Codex, usa su icono en la barra lateral. Se abrirá un panel con una caja para escribirle: ahí pegaremos nuestro mensaje.

```scene
id: open-chat
type: visual
visual: open-chat
items:
- icon: 📂
  label: mis-videojuegos
```


### 7. Una biblioteca de videojuegos

Vamos a crear una biblioteca de videojuegos con portadas, búsqueda y favoritos. Tendremos usuarios normales y un administrador que podrá agregar, editar y eliminar juegos. También podremos cambiar de usuario con un clic.

```scene
id: game-library
type: visual
visual: app-preview
items:
- icon: 👤
  label: Usuario
- icon: 🛡️
  label: Administrador
```


### 8. ¿Qué es un navegador?

Antes, una pregunta: ¿qué es un navegador? Es el programa que nos permite acceder a internet y ver páginas, imágenes y videos. Y es muy importante, porque nos permite usar aplicaciones sin instalarlas en nuestra máquina: basta escribir una dirección y ya estamos dentro de una aplicación web.

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
  - Funciona sin ninguna dirección
  - Necesita instalar Docker primero
answer: 0
explanation: Con solo escribir una dirección ya estamos dentro de la aplicación, sin instalar nada.
```

### 9. Frontend: lo que ves

Una aplicación web moderna tiene varios componentes. El frontend, o cliente, es lo que vemos directamente en el navegador: los botones y los formularios con los que interactuamos. Lo construiremos con React.

```scene
id: concept-frontend
type: visual
visual: stack
focus: 0
items:
  - icon: 🖥️
    label: Frontend
    detail: React · lo que ves
  - icon: ⚙️
    label: Backend
    detail: ASP.NET Core · recibe peticiones
  - icon: 🗄️
    label: Base de datos
    detail: SQLite · guarda la información
  - icon: 🐳
    label: Docker
    detail: ejecuta todo en contenedores
```

### 10. Backend: quien recibe las peticiones

El backend, o servidor, es el encargado de recibir las peticiones del navegador. Por ejemplo: muéstrame la información, modifícame este campo, guárdame esto, bórrame aquello. Recibe la petición, hace las validaciones y ejecuta las acciones. Usaremos ASP.NET Core.

```scene
id: concept-backend
type: visual
visual: stack
focus: 1
steps:
  - Muéstrame la información
  - Modifica este campo
  - Guarda esto
  - Borra aquello
items:
  - icon: 🖥️
    label: Frontend
    detail: React · lo que ves
  - icon: ⚙️
    label: Backend
    detail: ASP.NET Core · recibe peticiones
  - icon: 🗄️
    label: Base de datos
    detail: SQLite · guarda la información
  - icon: 🐳
    label: Docker
    detail: ejecuta todo en contenedores
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

### 11. Base de datos: donde se guarda

La base de datos es la que usa el backend para persistir, es decir, guardar la información como tal. Usaremos SQLite.

```scene
id: concept-database
type: visual
visual: stack
focus: 2
items:
  - icon: 🖥️
    label: Frontend
    detail: React · lo que ves
  - icon: ⚙️
    label: Backend
    detail: ASP.NET Core · recibe peticiones
  - icon: 🗄️
    label: Base de datos
    detail: SQLite · guarda la información
  - icon: 🐳
    label: Docker
    detail: ejecuta todo en contenedores
```

```exercise
id: quiz-database
type: multiple-choice
prompt: Si el backend no guardara nada en la base de datos, ¿qué pasaría?
choices:
  - Los juegos y favoritos se perderían al reiniciar
  - La aplicación se vería distinta
  - Docker dejaría de funcionar
answer: 0
explanation: Persistir significa guardar la información para que siga ahí cuando reiniciamos.
```

### 12. Docker: la caja que lo contiene

Además usaremos Docker, que nos permite ejecutar la aplicación en contenedores, sin tener que instalar cosas directamente en nuestra máquina. Un contenedor reúne toda nuestra aplicación y sus dependencias, y funciona igual en cualquier computador, sin importar el sistema operativo. Así no tenemos que instalar nada y, además, podremos llevar la aplicación a cualquier lado.

```scene
id: concept-docker
type: visual
visual: stack
focus: 3
items:
  - icon: 🖥️
    label: Frontend
    detail: React · lo que ves
  - icon: ⚙️
    label: Backend
    detail: ASP.NET Core · recibe peticiones
  - icon: 🗄️
    label: Base de datos
    detail: SQLite · guarda la información
  - icon: 🐳
    label: Docker
    detail: ejecuta todo en contenedores
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

### 13. Autoriza, copia y envía

Vamos a pedirle al agente que construya la aplicación y prepare todo lo necesario para ejecutarla. Eso puede incluir instalar programas en tu computador. Lee la autorización y, si estás de acuerdo, marca Acepto, copia el mensaje y envíalo.

```scene
id: authorize-prompt
type: visual
visual: prompt-flow
items:
- icon: ☑️
  label: 1. Acepto
- icon: 📋
  label: 2. Copiar
- icon: 💬
  label: 3. Pegar y enviar
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
explanation: Copiar no ejecuta nada. Solo marcas «Acepto» si estás de acuerdo y luego envías el mensaje
  al agente.
```

### 14. El agente construye la aplicación

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

### 15. Verifica la aplicación

Ya tenemos una aplicación, y el agente la dejó corriendo. Tú solo abre el navegador y escribe la dirección que te dio, por ejemplo localhost dos puntos tres mil. Ahora comprueba la aplicación: usa sus botones, cambia de usuario y prueba sus funciones. Si algo falla, díselo al agente para que lo corrija. Y si la aplicación no está corriendo, también se lo puedes pedir: dile que la ejecute y te dé la dirección.

```scene
id: verify-app
type: visual
visual: app-preview
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

### 16. Tu primer cambio

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

### 17. De una carpeta vacía a una aplicación

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


## Entregables de AutoTorial

- Lección audiovisual e interactiva con instrucciones para Windows, macOS y Linux.
- Autorización obligatoria antes de copiar el prompt.
- Tres ejercicios con instrucciones copiables.
- Publicación con `.autotorial/deploy-pages` y verificación de videos, interacciones y botones de copiar.
