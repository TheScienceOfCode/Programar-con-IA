---
title: "Lección 0: Primer contacto con el computador para programar"
courseTitle: "Aprende a\nProgramar con IA"
language: es
objectives:
  - Preparar un editor y conectar un agente de programación
  - Construir y verificar una biblioteca web de videojuegos con ayuda de IA
  - Solicitar y comprobar un primer cambio en la aplicación
prerequisites:
  - Ninguno
---

# Lección 0 — Primer contacto con el computador para programar

**Proyecto:** Aprende a Programar con IA  
**Formato:** video guiado + pasos interactivos  
**Público:** principiantes absolutos  
**Objetivo:** construir y modificar una biblioteca de videojuegos utilizando un agente de IA.

## Instrucciones para AutoTorial

Produce esta lección utilizando el flujo existente de AutoTorial. Usa capturas reales, animaciones sencillas y narración breve. Evita explicaciones técnicas innecesarias.

## Guion

### 1. ¿Por qué aprender a programar con IA?

**Visual:** computador antiguo → editor moderno → agentes trabajando → aplicación terminada.

**Narración:**

Los computadores han ampliado nuestra capacidad de calcular, recordar y resolver problemas.

Ahora la inteligencia artificial nos permite ir más allá: podemos describir una idea y trabajar con agentes capaces de escribir programas, encontrar errores y proponer soluciones.

Incluso podemos tener varios agentes trabajando en diferentes tareas. No son infalibles, pero multiplican lo que podemos crear.

Vamos a probarlo.

### 2. Preparar el editor

**Visual:** selector de Windows, macOS y Linux. Demostración de instalación o apertura.

**Narración:**

Necesitamos un editor para trabajar con nuestros archivos y conversar con el agente. Usaremos Visual Studio Code; en Linux también puedes utilizar VSCodium.

Entra a code.visualstudio.com/download y elige tu sistema: Windows, macOS o Linux.

Ahora instálalo. En Windows, abre el instalador y pulsa Siguiente hasta terminar. En macOS, arrastra Visual Studio Code a Aplicaciones. En Linux, instala el paquete con apt (Ubuntu/Debian) o dnf (Fedora). Cuando termine, ábrelo. Si ya lo tienes, salta este paso.

**Enlaces:**
- VS Code: https://code.visualstudio.com/download
- VSCodium: https://vscodium.com/

**Notas:** incluir «Ya lo tengo» para saltar este paso. En Linux, adaptar la instalación a la distribución.

### 3. Conectar nuestro agente

**Visual:** abrir Extensiones, instalar Codex o Claude Code, iniciar sesión y abrir el chat. Crear la carpeta `mis-videojuegos`.

**Narración:**

Abre el panel de extensiones (Ctrl+Shift+X), busca Codex o Claude Code, pulsa Instalar e inicia sesión.

Ahora crea una carpeta llamada `mis-videojuegos` y ábrela desde Archivo → Abrir carpeta. Ahí construiremos nuestra aplicación. Abre el chat del agente: ya está listo para escribirle.

**Nota:** verificar que la extensión funcione en el editor mostrado, especialmente en VSCodium.

### 4. ¿Qué vamos a construir?

**Visual:** catálogo de videojuegos inspirado en Steam, favoritos y cambio de usuario.

**Narración:**

Vamos a crear una biblioteca de videojuegos con portadas, búsqueda y favoritos.

Tendremos usuarios normales y un administrador que podrá agregar, editar y eliminar juegos. También podremos cambiar de usuario con un clic.

### 5. Cuatro conceptos rápidos

**Visual:** React ↔ ASP.NET Core ↔ SQLite. Docker alrededor de la aplicación.

**Narración:**

El frontend es lo que vemos y utilizamos en el navegador. Lo construiremos con React.

El backend gestiona las acciones y los datos. Usaremos ASP.NET Core.

SQLite guardará nuestra información, mientras Docker nos permitirá ejecutar la aplicación en contenedores.

No necesitas memorizarlo todavía.

### 6. Autorizar y enviar el prompt

**Visual:** aviso de autorización, casilla «Acepto» y botón «Copiar prompt».

**Narración:**

Vamos a pedirle al agente que construya la aplicación y prepare todo lo necesario para ejecutarla.

Eso puede incluir instalar programas en tu computador. Lee la autorización y, si estás de acuerdo, marca «Acepto», copia el mensaje y envíalo.

### 7. El agente construye la aplicación

**Visual:** chat del agente y terminal con `docker compose up`.

**Narración:**

Al enviar el mensaje, el agente trabaja solo: detecta tu sistema, instala lo que falte, escribe el código, ejecuta la aplicación con Docker y la prueba en el navegador. Puede tardar varios minutos y pedirte permisos. Léelos y acéptalos solo si estás de acuerdo.

### 8. Verificar nuestra aplicación

**Visual:** grabación real del agente construyendo el proyecto y de la aplicación funcionando en el navegador.

**Narración:**

Ya tenemos una aplicación. Ahora debemos comprobarla: abrirla, utilizar sus botones, cambiar de usuario y probar sus funciones.

Si algo falla, le pedimos al agente que lo corrija.

### 9. Tu primer cambio

**Visual:** tres ejercicios seleccionables con instrucciones copiables.

**Opciones:**

- **Colores:** «Agrega un botón para cambiar entre tema claro y oscuro y recuerda mi preferencia».
- **Puntuación:** «Permite que cada usuario puntúe los videojuegos de una a cinco estrellas».
- **Orden:** «Permite ordenar los videojuegos por título, año o género».

**Narración:**

Ahora te toca a ti. Elige un cambio, pídeselo al agente y comprueba el resultado en el navegador.

### 10. Cierre

**Visual:** editor y aplicación terminada.

**Narración:**

Empezamos con una carpeta vacía y terminamos con una aplicación que funciona.

Todavía no entendemos todo su código. En las siguientes lecciones aprenderemos a comprenderlo y a tomar mejores decisiones al trabajar con inteligencia artificial.

---

## Autorización antes de copiar el prompt

**Título:** Permiso para instalar software

**Aviso:**

Este mensaje autoriza al agente a instalar y configurar las herramientas necesarias para ejecutar el proyecto, incluido Docker.

Estas operaciones pueden modificar la configuración de tu computador y requerir permisos de administrador o reiniciar el sistema.

**Casilla (desmarcada inicialmente):**

«Acepto y autorizo estas instalaciones y configuraciones para este proyecto».

El botón **Copiar prompt** solo se habilita después de aceptar. Copiar el texto no lo ejecuta ni sustituye las aprobaciones que solicite el sistema operativo.

## Prompt completo para el estudiante

Quiero que construyas una biblioteca web de videojuegos. Soy principiante: haz el trabajo y explícame lo esencial con palabras sencillas.

**Tecnologías:** React.js (frontend), ASP.NET Core con C# (backend), SQLite (datos) y Docker Compose para ejecutarlo.

**Funcionalidades:**

- Catálogo con portada, título, año, género, plataforma y descripción, con búsqueda y filtros.
- Cuentas de demostración y botón **Cambiar usuario** para entrar con un clic.
- Administrador: agregar, editar y eliminar videojuegos.
- Usuario normal: explorar y marcar favoritos, sin editar el catálogo.
- Validar los permisos también en el backend.
- Conservar datos y favoritos al reiniciar.

**Diseño:** inspirado en Steam, tonos azules oscuros, portadas y adaptación a pantallas pequeñas.

**Videojuegos iniciales:**

- Commander Keen 4: Secret of the Oracle (1991).
- Another World (1991).
- Prince of Persia (1989).
- Prince of Persia 2: The Shadow and the Flame (1993).
- Super Mario World (1990).
- Simon the Sorcerer 2 (1995).

Utiliza portadas reales de fuentes accesibles o imágenes de reemplazo.

**Instalación:**

Te autorizo a instalar y configurar las dependencias necesarias, incluido Docker y sus componentes.

Detecta mi sistema operativo e instala lo que falte, sin limitarte a darme instrucciones. Si necesitas permisos de administrador o reiniciar, solicítame intervenir.

No borres archivos personales ni realices cambios ajenos al proyecto.

Trabaja en la carpeta actual, ejecuta la aplicación con Docker y dame la dirección para abrirla.

**Verificación:**

Antes de terminar, abre la aplicación en un navegador y comprueba que realmente funciona. Haz clic en los botones, cambia de usuario, agrega y edita videojuegos y prueba las funciones principales.

Si algo falla, corrígelo y vuelve a comprobar. Si no puedes controlar el navegador, indícalo y guíame para verificar la aplicación.

Al terminar, explícame brevemente qué construiste y cómo iniciar y detener la aplicación.

Toma decisiones razonables sin preguntarme cada detalle. Las cuentas de demostración son solo para uso educativo local.

---

## Entregables de AutoTorial

- Lección audiovisual e interactiva con instrucciones para Windows, macOS y Linux.
- Autorización obligatoria antes de copiar el prompt.
- Demostración real de construcción, funcionamiento y corrección de errores.
- Tres ejercicios con instrucciones copiables.
- Publicación utilizando el flujo existente de AutoTorial.
- Comprobación de reproducción de videos y funcionamiento de botones.

**Principio pedagógico:** primero construir algo útil; después aprender a entenderlo y dominarlo.

```autotorial
{
  "scenes": [
    {
      "id": "why-ai",
      "type": "visual",
      "visual": "timeline",
      "title": "De una idea a una aplicación",
      "items": [
        {
          "icon": "🖥️",
          "label": "Los computadores",
          "detail": "calculan y recuerdan"
        },
        {
          "icon": "✍️",
          "label": "Describes una idea",
          "detail": "con tus palabras"
        },
        {
          "icon": "🤖",
          "label": "Agentes de IA",
          "detail": "escriben y corrigen"
        },
        {
          "icon": "🎮",
          "label": "Aplicación terminada",
          "detail": "tú la compruebas"
        }
      ],
      "narration": "Los computadores han ampliado nuestra capacidad de calcular, recordar y resolver problemas. Ahora la inteligencia artificial nos permite ir más allá: podemos describir una idea y trabajar con agentes capaces de escribir programas, encontrar errores y proponer soluciones. Incluso podemos tener varios agentes trabajando en diferentes tareas. No son infalibles, pero multiplican lo que podemos crear. Vamos a probarlo."
    },
    {
      "id": "download-editor",
      "type": "visual",
      "visual": "browser-download",
      "title": "Descarga Visual Studio Code",
      "items": [
        {
          "icon": "🪟",
          "label": "Windows",
          "detail": "Instalador .exe"
        },
        {
          "icon": "🍎",
          "label": "macOS",
          "detail": "Archivo .zip"
        },
        {
          "icon": "🐧",
          "label": "Linux",
          "detail": ".deb · .rpm · VSCodium"
        }
      ],
      "narration": "Necesitamos un editor para trabajar con nuestros archivos y conversar con el agente. Usaremos Visual Studio Code; en Linux también puedes utilizar VSCodium. Entra a code punto visual studio punto com, barra download, y elige tu sistema: Windows, macOS o Linux."
    },
    {
      "id": "install-editor",
      "type": "visual",
      "visual": "installer",
      "title": "Instálalo y ábrelo",
      "items": [
        {
          "icon": "🪟",
          "label": "Windows",
          "steps": [
            "Abre VSCodeUserSetup.exe",
            "Acepta y pulsa Siguiente",
            "Pulsa Instalar",
            "Marca «Ejecutar» y Finalizar"
          ]
        },
        {
          "icon": "🍎",
          "label": "macOS",
          "steps": [
            "Abre el .zip descargado",
            "Arrastra VS Code a Aplicaciones",
            "Ábrelo desde Launchpad",
            "Pulsa «Abrir» si macOS lo pide"
          ]
        },
        {
          "icon": "🐧",
          "label": "Linux",
          "steps": [
            "$ sudo apt install ./code_*.deb",
            "$ sudo dnf install ./code-*.rpm",
            "Ábrelo desde el menú de aplicaciones"
          ]
        }
      ],
      "narration": "Ahora instálalo. En Windows, abre el instalador y pulsa Siguiente hasta terminar. En macOS, abre el archivo descargado y arrastra Visual Studio Code a la carpeta Aplicaciones. En Linux, instala el paquete: con apt en Ubuntu y Debian, o con dnf en Fedora. Cuando termine, ábrelo. Si ya lo tienes, salta este paso."
    },
    {
      "id": "install-extension",
      "type": "visual",
      "visual": "extensions",
      "title": "Instala tu agente",
      "items": [
        {
          "icon": "🟠",
          "label": "Claude Code",
          "detail": "Anthropic"
        },
        {
          "icon": "⚫",
          "label": "Codex",
          "detail": "OpenAI"
        }
      ],
      "narration": "Abre el panel de extensiones, con el icono de cuadritos o con Control, Shift y X. Busca Codex o Claude Code y pulsa Instalar. Después inicia sesión con tu cuenta."
    },
    {
      "id": "open-folder",
      "type": "visual",
      "visual": "open-folder",
      "title": "Abre tu carpeta de trabajo",
      "items": [
        {
          "icon": "📂",
          "label": "mis-videojuegos"
        }
      ],
      "narration": "Ahora crea una carpeta llamada mis-videojuegos y ábrela desde el menú Archivo, Abrir carpeta. Ahí construiremos nuestra aplicación. Abre el chat del agente: ya está listo para escribirle."
    },
    {
      "id": "game-library",
      "type": "visual",
      "visual": "app-preview",
      "title": "Una biblioteca de videojuegos",
      "items": [
        {
          "icon": "👤",
          "label": "Usuario"
        },
        {
          "icon": "🛡️",
          "label": "Administrador"
        }
      ],
      "narration": "Vamos a crear una biblioteca de videojuegos con portadas, búsqueda y favoritos. Tendremos usuarios normales y un administrador que podrá agregar, editar y eliminar juegos. También podremos cambiar de usuario con un clic."
    },
    {
      "id": "four-concepts",
      "type": "diagram",
      "title": "Cuatro conceptos rápidos",
      "nodes": [
        {
          "id": "frontend",
          "label": "React · lo que ves"
        },
        {
          "id": "backend",
          "label": "ASP.NET Core · acciones"
        },
        {
          "id": "data",
          "label": "SQLite · datos"
        },
        {
          "id": "containers",
          "label": "Docker · ejecución"
        }
      ],
      "edges": [
        [
          "frontend",
          "backend"
        ],
        [
          "backend",
          "data"
        ],
        [
          "containers",
          "frontend"
        ]
      ],
      "narration": "El frontend es lo que vemos y utilizamos en el navegador. Lo construiremos con React. El backend gestiona las acciones y los datos. Usaremos ASP.NET Core. SQLite guardará nuestra información, mientras Docker nos permitirá ejecutar la aplicación en contenedores. No necesitas memorizarlo todavía."
    },
    {
      "id": "authorize-prompt",
      "type": "visual",
      "visual": "prompt-flow",
      "title": "Autoriza, copia y envía",
      "items": [
        {
          "icon": "☑️",
          "label": "1. Acepto"
        },
        {
          "icon": "📋",
          "label": "2. Copiar"
        },
        {
          "icon": "💬",
          "label": "3. Pegar y enviar"
        }
      ],
      "narration": "Vamos a pedirle al agente que construya la aplicación y prepare todo lo necesario para ejecutarla. Eso puede incluir instalar programas en tu computador. Lee la autorización y, si estás de acuerdo, marca Acepto, copia el mensaje y envíalo."
    },
    {
      "id": "agent-builds",
      "type": "visual",
      "visual": "agent-work",
      "title": "El agente construye la aplicación",
      "steps": [
        "Detecté tu sistema operativo",
        "Instalé Docker y sus componentes",
        "Escribí el backend y el frontend",
        "Ejecuté la aplicación con Docker",
        "La probé en el navegador"
      ],
      "narration": "Al enviar el mensaje, el agente trabaja solo: detecta tu sistema, instala lo que falte, escribe el código, ejecuta la aplicación con Docker y la prueba en el navegador. Puede tardar varios minutos y pedirte permisos. Léelos y acéptalos solo si estás de acuerdo."
    },
    {
      "id": "verify-app",
      "type": "visual",
      "visual": "app-preview",
      "title": "Verifica la aplicación",
      "items": [
        {
          "icon": "👤",
          "label": "Usuario"
        },
        {
          "icon": "🛡️",
          "label": "Administrador"
        }
      ],
      "steps": [
        "Abre la aplicación",
        "Cambia de usuario",
        "Marca favoritos",
        "Agrega, edita y elimina"
      ],
      "narration": "Ya tenemos una aplicación. Ahora debemos comprobarla: abrirla, utilizar sus botones, cambiar de usuario y probar sus funciones. Si algo falla, le pedimos al agente que lo corrija."
    },
    {
      "id": "first-change",
      "type": "visual",
      "visual": "choices",
      "title": "Tu primer cambio",
      "items": [
        {
          "icon": "🌗",
          "label": "Colores",
          "detail": "Agrega un botón para cambiar entre tema claro y oscuro"
        },
        {
          "icon": "⭐",
          "label": "Puntuación",
          "detail": "Permite puntuar los videojuegos de una a cinco estrellas"
        },
        {
          "icon": "🔀",
          "label": "Orden",
          "detail": "Permite ordenar por título, año o género"
        }
      ],
      "narration": "Ahora te toca a ti. Elige un cambio, pídeselo al agente y comprueba el resultado en el navegador."
    },
    {
      "id": "closing",
      "type": "visual",
      "visual": "timeline",
      "title": "De una carpeta vacía a una aplicación",
      "items": [
        {
          "icon": "📂",
          "label": "Carpeta vacía"
        },
        {
          "icon": "💬",
          "label": "Un prompt"
        },
        {
          "icon": "🤖",
          "label": "El agente construye"
        },
        {
          "icon": "✅",
          "label": "Aplicación que funciona"
        }
      ],
      "narration": "Empezamos con una carpeta vacía y terminamos con una aplicación que funciona. Todavía no entendemos todo su código. En las siguientes lecciones aprenderemos a comprenderlo y a tomar mejores decisiones al trabajar con inteligencia artificial."
    }
  ],
  "exercises": [
    {
      "id": "quiz-why-ai",
      "type": "multiple-choice",
      "afterScene": "why-ai",
      "prompt": "¿Qué papel tiene la inteligencia artificial en este curso?",
      "choices": [
        "Reemplaza por completo a la persona, que ya no debe revisar nada",
        "Trabaja como agente que escribe y corrige programas, y tú compruebas el resultado",
        "Sirve únicamente para buscar información en internet"
      ],
      "answer": 1,
      "explanation": "Los agentes multiplican lo que podemos crear, pero no son infalibles: siempre comprobamos el resultado."
    },
    {
      "id": "quiz-download-editor",
      "type": "multiple-choice",
      "afterScene": "download-editor",
      "prompt": "¿De dónde descargas Visual Studio Code?",
      "choices": [
        "De un correo que te envía el agente",
        "De code.visualstudio.com/download",
        "De la carpeta mis-videojuegos"
      ],
      "answer": 1,
      "explanation": "El instalador oficial está en code.visualstudio.com/download; en Linux también puedes usar VSCodium."
    },
    {
      "id": "quiz-install-editor",
      "type": "multiple-choice",
      "afterScene": "install-editor",
      "prompt": "¿Cómo instalas Visual Studio Code en macOS?",
      "choices": [
        "Arrastrándolo a la carpeta Aplicaciones",
        "Escribiendo sudo dnf install",
        "Ejecutando docker compose up"
      ],
      "answer": 0,
      "explanation": "En macOS se abre el archivo descargado y se arrastra la aplicación a Aplicaciones."
    },
    {
      "id": "quiz-install-extension",
      "type": "multiple-choice",
      "afterScene": "install-extension",
      "prompt": "¿Dónde buscas Codex o Claude Code dentro del editor?",
      "choices": [
        "En el panel de Extensiones (Ctrl+Shift+X)",
        "En el menú Archivo → Guardar",
        "En el navegador de la aplicación"
      ],
      "answer": 0,
      "explanation": "Se instalan desde el panel de Extensiones y luego inicias sesión con tu cuenta."
    },
    {
      "id": "quiz-open-folder",
      "type": "multiple-choice",
      "afterScene": "open-folder",
      "prompt": "¿Qué carpeta abres para construir la aplicación?",
      "choices": [
        "Documentos",
        "Descargas",
        "mis-videojuegos"
      ],
      "answer": 2,
      "explanation": "Ahí construiremos la aplicación: en Archivo → Abrir carpeta eliges mis-videojuegos."
    },
    {
      "id": "quiz-game-library",
      "type": "multiple-choice",
      "afterScene": "game-library",
      "prompt": "¿Qué puede hacer el administrador de la biblioteca?",
      "choices": [
        "Solo marcar favoritos",
        "Agregar, editar y eliminar videojuegos",
        "Únicamente cambiar de usuario"
      ],
      "answer": 1,
      "explanation": "El administrador gestiona el catálogo; los usuarios normales exploran y guardan favoritos."
    },
    {
      "id": "quiz-four-concepts",
      "type": "multiple-choice",
      "afterScene": "four-concepts",
      "prompt": "¿Qué tecnología guarda la información de la aplicación?",
      "choices": [
        "React",
        "Docker",
        "SQLite"
      ],
      "answer": 2,
      "explanation": "SQLite guarda los datos. React construye lo que ves, ASP.NET Core gestiona las acciones y Docker ejecuta la aplicación."
    },
    {
      "id": "authorize-and-copy",
      "type": "authorization",
      "afterScene": "authorize-prompt",
      "prompt": "Permiso para instalar software",
      "notice": "Este mensaje autoriza al agente a instalar y configurar las herramientas necesarias para ejecutar el proyecto, incluido Docker. Estas operaciones pueden modificar la configuración de tu computador y requerir permisos de administrador o reiniciar el sistema.",
      "consentLabel": "Acepto y autorizo estas instalaciones y configuraciones para este proyecto.",
      "buttonLabel": "Copiar prompt completo",
      "copyText": "Quiero que construyas una biblioteca web de videojuegos. Soy principiante: haz el trabajo y explícame lo esencial con palabras sencillas.\n\nTecnologías: React.js (frontend), ASP.NET Core con C# (backend), SQLite (datos) y Docker Compose para ejecutarlo.\n\nFuncionalidades:\n- Catálogo con portada, título, año, género, plataforma y descripción, con búsqueda y filtros.\n- Cuentas de demostración y botón Cambiar usuario para entrar con un clic.\n- Administrador: agregar, editar y eliminar videojuegos.\n- Usuario normal: explorar y marcar favoritos, sin editar el catálogo.\n- Validar los permisos también en el backend.\n- Conservar datos y favoritos al reiniciar.\n\nDiseño: inspirado en Steam, tonos azules oscuros, portadas y adaptación a pantallas pequeñas.\n\nVideojuegos iniciales:\n- Commander Keen 4: Secret of the Oracle (1991).\n- Another World (1991).\n- Prince of Persia (1989).\n- Prince of Persia 2: The Shadow and the Flame (1993).\n- Super Mario World (1990).\n- Simon the Sorcerer 2 (1995).\n\nUtiliza portadas reales de fuentes accesibles o imágenes de reemplazo.\n\nInstalación:\nTe autorizo a instalar y configurar las dependencias necesarias, incluido Docker y sus componentes.\nDetecta mi sistema operativo e instala lo que falte, sin limitarte a darme instrucciones. Si necesitas permisos de administrador o reiniciar, solicítame intervenir.\nNo borres archivos personales ni realices cambios ajenos al proyecto.\nTrabaja en la carpeta actual, ejecuta la aplicación con Docker y dame la dirección para abrirla.\n\nVerificación:\nAntes de terminar, abre la aplicación en un navegador y comprueba que realmente funciona. Haz clic en los botones, cambia de usuario, agrega y edita videojuegos y prueba las funciones principales.\nSi algo falla, corrígelo y vuelve a comprobar. Si no puedes controlar el navegador, indícalo y guíame para verificar la aplicación.\n\nAl terminar, explícame brevemente qué construiste y cómo iniciar y detener la aplicación.\n\nToma decisiones razonables sin preguntarme cada detalle. Las cuentas de demostración son solo para uso educativo local.",
      "explanation": "El prompt quedó copiado. Pégalo en el chat del agente; copiarlo no ejecuta ninguna instalación."
    },
    {
      "id": "quiz-authorize-prompt",
      "type": "multiple-choice",
      "afterScene": "authorize-prompt",
      "prompt": "¿Qué ocurre al copiar el prompt?",
      "choices": [
        "Se instala todo automáticamente en ese momento",
        "No se ejecuta nada: el agente actúa solo cuando tú lo envías, y el sistema aún puede pedir permisos",
        "El computador se reinicia"
      ],
      "answer": 1,
      "explanation": "Copiar no ejecuta nada. Solo marcas «Acepto» si estás de acuerdo y luego envías el mensaje al agente."
    },
    {
      "id": "quiz-agent-builds",
      "type": "multiple-choice",
      "afterScene": "agent-builds",
      "prompt": "Mientras el agente trabaja, ¿qué haces si te pide permisos?",
      "choices": [
        "Los lees y aceptas solo si estás de acuerdo",
        "Los aceptas sin leer",
        "Cierras el editor"
      ],
      "answer": 0,
      "explanation": "Puede pedir permisos para instalar o ejecutar cosas: léelos antes de aceptar."
    },
    {
      "id": "quiz-verify-app",
      "type": "multiple-choice",
      "afterScene": "verify-app",
      "prompt": "¿Qué haces cuando algo de la aplicación no funciona?",
      "choices": [
        "Lo ignoras y sigues",
        "Se lo pides al agente para que lo corrija y vuelves a comprobar",
        "Borras la carpeta y empiezas de nuevo"
      ],
      "answer": 1,
      "explanation": "Si algo falla, le pedimos al agente que lo corrija y comprobamos otra vez."
    },
    {
      "id": "change-colors",
      "type": "prompt-copy",
      "afterScene": "first-change",
      "prompt": "Opción 1: colores",
      "copyText": "Agrega un botón para cambiar entre tema claro y oscuro y recuerda mi preferencia. Comprueba el cambio en el navegador y corrige cualquier problema que encuentres.",
      "explanation": "Instrucción copiada. Pégala en el chat del agente y comprueba ambos temas."
    },
    {
      "id": "change-rating",
      "type": "prompt-copy",
      "afterScene": "first-change",
      "prompt": "Opción 2: puntuación",
      "copyText": "Permite que cada usuario puntúe los videojuegos de una a cinco estrellas. Conserva las puntuaciones al reiniciar y comprueba el cambio en el navegador.",
      "explanation": "Instrucción copiada. Pégala en el chat del agente y prueba varias puntuaciones."
    },
    {
      "id": "change-order",
      "type": "prompt-copy",
      "afterScene": "first-change",
      "prompt": "Opción 3: orden",
      "copyText": "Permite ordenar los videojuegos por título, año o género. Comprueba cada opción en el navegador y corrige cualquier problema que encuentres.",
      "explanation": "Instrucción copiada. Pégala en el chat del agente y prueba los tres criterios."
    },
    {
      "id": "quiz-first-change",
      "type": "multiple-choice",
      "afterScene": "first-change",
      "prompt": "¿Cómo compruebas que tu primer cambio quedó bien?",
      "choices": [
        "Confiando en que el agente no se equivoca",
        "Abriendo la aplicación en el navegador y probando el cambio",
        "Leyendo todo el código"
      ],
      "answer": 1,
      "explanation": "Siempre se comprueba el resultado en el navegador."
    },
    {
      "id": "quiz-closing",
      "type": "multiple-choice",
      "afterScene": "closing",
      "prompt": "¿Qué aprenderemos en las siguientes lecciones?",
      "choices": [
        "A comprender el código y a tomar mejores decisiones con inteligencia artificial",
        "A instalar otro editor",
        "A no volver a usar agentes"
      ],
      "answer": 0,
      "explanation": "Empezamos construyendo; ahora toca entender lo construido."
    }
  ]
}
```
