# Programar-con-IA
Aprende a Programar con IA

## Autotorial

El generador de lecciones está instalado como submódulo en `lib/autotorial`.
El comando local del proyecto es `.autotorial/autotorial` y los artefactos
generados se guardan en `bin/autotorial/`.

Inicializa una copia nueva del proyecto con:

```bash
git submodule sync --recursive
git submodule update --init --recursive
npm ci --prefix lib/autotorial
npm run build --prefix lib/autotorial
./lib/autotorial/install.sh
```

Flujo básico:

```bash
.autotorial/autotorial validate session-1
.autotorial/autotorial produce session-1
.autotorial/autotorial preview --port 4173
.autotorial/autotorial publish
```

Las definiciones estructuradas dentro de cada `lessons/<sesión>/INDEX.md`
usan un bloque JSON cercado con el identificador `autotorial`. Consulta
`lib/autotorial/docs/LESSON_FORMAT.md` para el formato completo.
