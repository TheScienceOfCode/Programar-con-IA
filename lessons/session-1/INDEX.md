---
title: "Lección 0: Primer contacto con el computador para programar"
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

Instálalo y ábrelo.

**Enlaces:**
- VS Code: https://code.visualstudio.com/download
- VSCodium: https://vscodium.com/

**Notas:** incluir «Ya lo tengo» para saltar este paso. En Linux, adaptar la instalación a la distribución.

### 3. Conectar nuestro agente

**Visual:** abrir Extensiones, instalar Codex o Claude Code, iniciar sesión y abrir el chat. Crear la carpeta `mis-videojuegos`.

**Narración:**

Instala Codex o Claude Code desde las extensiones del editor e inicia sesión.

Luego crea y abre una carpeta llamada `mis-videojuegos`. Ahí construiremos nuestra aplicación.

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

### 7. Verificar nuestra aplicación

**Visual:** grabación real del agente construyendo el proyecto y de la aplicación funcionando en el navegador.

**Narración:**

Ya tenemos una aplicación. Ahora debemos comprobarla: abrirla, utilizar sus botones, cambiar de usuario y probar sus funciones.

Si algo falla, le pedimos al agente que lo corrija.

### 8. Tu primer cambio

**Visual:** tres ejercicios seleccionables con instrucciones copiables.

**Opciones:**

- **Colores:** «Agrega un botón para cambiar entre tema claro y oscuro y recuerda mi preferencia».
- **Puntuación:** «Permite que cada usuario puntúe los videojuegos de una a cinco estrellas».
- **Orden:** «Permite ordenar los videojuegos por título, año o género».

**Narración:**

Ahora te toca a ti. Elige un cambio, pídeselo al agente y comprueba el resultado en el navegador.

### 9. Cierre

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
      "type": "concept",
      "title": "De una idea a una aplicación",
      "body": "Los agentes de inteligencia artificial pueden ayudarnos a escribir programas, encontrar errores y proponer soluciones.",
      "bullets": ["Describe lo que quieres crear", "Trabaja con uno o varios agentes", "Comprueba siempre el resultado"],
      "narration": "Los computadores han ampliado nuestra capacidad de calcular, recordar y resolver problemas. Ahora la inteligencia artificial nos permite ir más allá: podemos describir una idea y trabajar con agentes capaces de escribir programas, encontrar errores y proponer soluciones. Incluso podemos tener varios agentes trabajando en diferentes tareas. No son infalibles, pero multiplican lo que podemos crear. Vamos a probarlo."
    },
    {
      "id": "prepare-editor",
      "type": "concept",
      "title": "Prepara el editor",
      "body": "Usaremos Visual Studio Code. En Linux también puedes utilizar VSCodium.",
      "bullets": ["Windows y macOS: code.visualstudio.com/download", "Linux: VS Code o vscodium.com", "Si ya lo tienes, continúa con el siguiente paso"],
      "narration": "Necesitamos un editor para trabajar con nuestros archivos y conversar con el agente. Usaremos Visual Studio Code; en Linux también puedes utilizar VSCodium. Instálalo y ábrelo."
    },
    {
      "id": "connect-agent",
      "type": "concept",
      "title": "Conecta tu agente",
      "body": "Abre Extensiones, instala Codex o Claude Code e inicia sesión.",
      "bullets": ["Abre el chat del agente", "Crea la carpeta mis-videojuegos", "Abre esa carpeta en el editor"],
      "narration": "Instala Codex o Claude Code desde las extensiones del editor e inicia sesión. Luego crea y abre una carpeta llamada mis-videojuegos. Ahí construiremos nuestra aplicación."
    },
    {
      "id": "game-library",
      "type": "concept",
      "title": "Una biblioteca de videojuegos",
      "body": "Crearemos un catálogo inspirado en Steam con portadas, búsqueda, favoritos y cambio de usuario.",
      "bullets": ["Usuarios normales exploran y guardan favoritos", "El administrador gestiona el catálogo", "Cambia de usuario con un clic"],
      "narration": "Vamos a crear una biblioteca de videojuegos con portadas, búsqueda y favoritos. Tendremos usuarios normales y un administrador que podrá agregar, editar y eliminar juegos. También podremos cambiar de usuario con un clic."
    },
    {
      "id": "four-concepts",
      "type": "diagram",
      "title": "Cuatro conceptos rápidos",
      "nodes": [
        {"id": "frontend", "label": "React · lo que ves"},
        {"id": "backend", "label": "ASP.NET Core · acciones"},
        {"id": "data", "label": "SQLite · datos"},
        {"id": "containers", "label": "Docker · ejecución"}
      ],
      "edges": [["frontend", "backend"], ["backend", "data"], ["containers", "frontend"]],
      "narration": "El frontend es lo que vemos y utilizamos en el navegador. Lo construiremos con React. El backend gestiona las acciones y los datos. Usaremos ASP.NET Core. SQLite guardará nuestra información, mientras Docker nos permitirá ejecutar la aplicación en contenedores. No necesitas memorizarlo todavía."
    },
    {
      "id": "authorize-prompt",
      "type": "concept",
      "title": "Autoriza y envía el prompt",
      "body": "El mensaje puede pedir al agente que instale herramientas. Lee el aviso antes de copiarlo.",
      "bullets": ["La casilla empieza desmarcada", "Copiar no ejecuta el mensaje", "El sistema operativo aún puede pedir permisos"],
      "narration": "Vamos a pedirle al agente que construya la aplicación y prepare todo lo necesario para ejecutarla. Eso puede incluir instalar programas en tu computador. Lee la autorización y, si estás de acuerdo, marca Acepto, copia el mensaje y envíalo."
    },
    {
      "id": "verify-app",
      "type": "terminal",
      "title": "Verifica la aplicación",
      "command": "docker compose up --build",
      "output": "✓ catálogo visible\n✓ cambio de usuario\n✓ favoritos\n✓ crear, editar y eliminar como administrador",
      "narration": "Ya tenemos una aplicación. Ahora debemos comprobarla: abrirla, utilizar sus botones, cambiar de usuario y probar sus funciones. Si algo falla, le pedimos al agente que lo corrija."
    },
    {
      "id": "first-change",
      "type": "concept",
      "title": "Tu primer cambio",
      "body": "Elige una mejora, copia su instrucción y comprueba el resultado en el navegador.",
      "bullets": ["Tema claro y oscuro", "Puntuación de una a cinco estrellas", "Orden por título, año o género"],
      "narration": "Ahora te toca a ti. Elige un cambio, pídeselo al agente y comprueba el resultado en el navegador."
    },
    {
      "id": "closing",
      "type": "concept",
      "title": "De una carpeta vacía a una aplicación",
      "body": "Construiste algo útil y comprobaste su funcionamiento con ayuda de inteligencia artificial.",
      "bullets": ["En las siguientes lecciones comprenderás el código", "Aprenderás a tomar mejores decisiones", "Seguirás mejorando la aplicación"],
      "narration": "Empezamos con una carpeta vacía y terminamos con una aplicación que funciona. Todavía no entendemos todo su código. En las siguientes lecciones aprenderemos a comprenderlo y a tomar mejores decisiones al trabajar con inteligencia artificial."
    }
  ],
  "exercises": [
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
    }
  ]
}
```
