---
title: "Lección 2: Acercándonos al código"
courseTitle: "Aprende a\nProgramar con IA"
language: es
objectives:
  - Reconocer los tipos nativos y las funciones
  - Entender qué es una clase: datos y funciones agrupados
  - Leer y escribir métodos de una clase
  - Predecir la ejecución de un programa y evitar errores comunes
prerequisites:
  - Lección 1
  - Editor con agente de programación
---

# Lección 2 — Acercándonos al código

**Formato:** una pantalla por cada `###`, con narración y escena visual. Las preguntas se hacen después de la narración.

**Criterio audiovisual:** lo que aparece entre el título de cada pantalla y `scene` es lo único que se narra. No narrar fragmentos de código ni instrucciones de producción. La narración es texto hablado, sin formato Markdown. Los ejemplos son didácticos y no están en el repositorio.

**Objetivo:** que alguien sin experiencia entienda los bloques básicos hasta llegar a una clase, y practique escribiendo y comprobando código.

## Partes

### 1. Tipos y funciones

#### Los tipos nativos

En esta lección nos vamos a acercar al código. Necesitamos unos bloques básicos, y los vamos a ver rápido hasta llegar a una clase. Después vas a practicar tú. Empecemos por los tipos nativos, que dicen qué clase de dato guardamos. Int es para números enteros. Float, double y decimal son para números con decimales: float y double los guardan con distinta precisión, y decimal es el más exacto, ideal para dinero. Char guarda un solo carácter, y string guarda texto.

```scene
id: tipos-nativos
type: code
language: csharp
focus:
  - lines: [1]
    at: "Int es para números enteros"
  - lines: [2, 3, 4]
    at: "Float, double y decimal"
  - lines: [4]
    at: "decimal es el más exacto"
  - lines: [5]
    at: "Char guarda un solo carácter"
  - lines: [6]
    at: "string guarda texto"
code: |-
  int edad = 30;                 // número entero
  float altura = 1.75f;          // decimal, poca precisión
  double distancia = 384400.5;   // decimal, más precisión
  decimal precio = 19.99m;       // decimal exacto, ideal para dinero
  char letra = 'A';              // un solo carácter
  string nombre = "Ana";         // texto
```

#### Funciones y métodos

Luego están las funciones, también llamadas métodos. Una función agrupa instrucciones bajo un nombre. Recibe datos de entrada, que llamamos parámetros, y puede devolver un resultado. Por ejemplo, sumar recibe dos números, a y b, y devuelve su suma. Después la llamamos con valores concretos y obtenemos el resultado.

```scene
id: funcion-sumar
type: code
language: csharp
focus:
  - lines: [1, 2, 3, 4]
    at: "Una función agrupa instrucciones"
  - lines: [1]
    at: "Recibe datos de entrada"
  - lines: [3]
    at: "puede devolver un resultado"
  - lines: [1, 3]
    at: "Por ejemplo, sumar"
  - lines: [6]
    at: "Después la llamamos"
code: |-
  int Sumar(int a, int b)
  {
      return a + b;
  }

  int resultado = Sumar(2, 3);
```

### 2. Bloques de control

```exercise
id: control-suma
type: code-completion
language: csharp
prompt: "Completa la función Sumar(a, b): debe devolver la suma de todos los números desde a hasta b, incluidos los dos. Usa un for."
starter: |-
  int Sumar(int a, int b)
  {
      int total = 0;
      // recorre desde a hasta b con un for
      // y suma cada número a total
      return total;
  }
solution: |-
  int Sumar(int a, int b)
  {
      int total = 0;
      for (int i = a; i <= b; i++)
      {
          total += i;
      }
      return total;
  }
tests:
  - name: "de 1 a 4 suma 10"
    expression: |-
      Console.WriteLine(Sumar(1, 4));
    expected: "10"
  - name: "de 3 a 5 suma 12"
    expression: |-
      Console.WriteLine(Sumar(3, 5));
    expected: "12"
  - name: "de 5 a 5 suma 5"
    expression: |-
      Console.WriteLine(Sumar(5, 5));
    expected: "5"
explanation: "El for recorre los números desde a hasta b y total va acumulando la suma."
```

#### if: tomar decisiones

Los bloques de control deciden qué se ejecuta y cuántas veces. El primero es if: ejecuta unas instrucciones solo si se cumple una condición. Aquí, si la edad es mayor o igual a dieciocho, mostramos que es mayor de edad. Con else decimos qué hacer en caso contrario.

```scene
id: control-if
type: code
language: csharp
focus:
  - lines: [3]
    at: "El primero es if"
  - lines: [5]
    at: "mostramos que es mayor de edad"
  - lines: [7, 8, 9, 10]
    at: "Con else"
code: |-
  int edad = 20;

  if (edad >= 18)
  {
      Console.WriteLine("Mayor de edad");
  }
  else
  {
      Console.WriteLine("Menor de edad");
  }
```

#### while: repetir mientras se cumpla

El bloque while repite instrucciones mientras una condición sea verdadera. En este ejemplo, mientras el contador sea menor que tres, mostramos el valor y lo aumentamos en uno. Cuando llega a tres, la condición deja de cumplirse y el ciclo termina. Cuidado: si nunca dejara de cumplirse, el programa se quedaría repitiendo para siempre.

```scene
id: control-while
type: code
language: csharp
focus:
  - lines: [3]
    at: "mientras el contador sea menor que tres"
  - lines: [5]
    at: "mostramos el valor"
  - lines: [6]
    at: "lo aumentamos en uno"
  - lines: [3]
    at: "la condición deja de cumplirse"
code: |-
  int contador = 0;

  while (contador < 3)
  {
      Console.WriteLine(contador);
      contador++;
  }
```

#### for: repetir un número de veces

El bloque for es una forma compacta de repetir cuando sabemos cuántas veces. Tiene tres partes: dónde empezamos, hasta cuándo seguimos y cómo avanzamos. Aquí empezamos en cero, seguimos mientras sea menor que tres y avanzamos de uno en uno. Hace lo mismo que el while anterior, pero en una sola línea. Ahora practica tú, aquí mismo en el navegador: completa la función que suma los números desde a hasta b. Se ejecuta como C# de verdad.

```scene
id: control-for
type: code
language: csharp
focus:
  - lines: [1]
    at: "Tiene tres partes"
  - lines: [1]
    at: "empezamos en cero"
  - lines: [3]
    at: "Hace lo mismo"
code: |-
  for (int i = 0; i < 3; i++)
  {
      Console.WriteLine(i);
  }
```

### 3. La clase

```exercise
id: oop-check
type: multiple-choice
prompt: "En una clase, ¿qué diferencia hay entre un atributo y un método?"
choices:
  - "El atributo contiene un dato; el método realiza una acción"
  - "Ambos son nombres para una base de datos"
  - "El método contiene datos y el atributo ejecuta acciones"
answer: 0
explanation: "La lista de nombres es un dato de la clase; agregar un nombre es una acción."
```

#### La clase

Ahora juntamos datos y funciones en una clase. Una clase no es más que datos y funciones agrupados. Aquí, la clase OperacionSuma tiene dos datos, A y B, que llamamos atributos o propiedades, y una función, Sumar, que usa esos datos y devuelve el resultado.

```scene
id: clase-operacion-suma
type: code
language: csharp
focus:
  - lines: [1, 2, 10]
    at: "Ahora juntamos datos y funciones"
  - lines: [3, 4]
    at: "tiene dos datos"
  - lines: [6, 7, 8, 9]
    at: "y una función, Sumar"
code: |-
  public class OperacionSuma
  {
      public int A { get; set; }
      public int B { get; set; }

      public int Sumar()
      {
          return A + B;
      }
  }
```

#### Public, get y set

Veamos dos detalles de la sintaxis. Public significa que se puede acceder desde cualquier parte de la aplicación. Si hubiese algo que queremos ocultar del resto de la aplicación, lo marcaríamos como private, pero son temas de diseño que veremos más adelante. Y get y set indican cómo se usa una propiedad: get permite leer su valor, y set permite cambiarlo.

```scene
id: public-get-set
type: code
language: csharp
focus:
  - lines: [1, 3, 4, 6]
    at: "Public significa que se puede acceder"
  - lines: [3, 4]
    at: "get y set indican"
  - lines: [3]
    at: "get permite leer su valor"
  - lines: [4]
    at: "set permite cambiarlo"
code: |-
  public class OperacionSuma     // public: accesible desde cualquier parte
  {
      public int A { get; set; } // get: leer el valor, set: cambiarlo
      public int B { get; set; }

      public int Sumar()
      {
          return A + B;
      }
  }
```

### 4. El código en VS Code

Así se vería esa clase en VS Code. A la izquierda está el explorador, con los archivos del proyecto. Arriba, la pestaña muestra el nombre del archivo: cada clase suele vivir en su propio archivo con extensión .cs, de C#. Y en el centro está el código.

```scene
id: vscode-ejemplo
type: visual
visual: vscode
header: MiProyecto
focus: 1
stepAt:
  - "A la izquierda"
  - "Arriba, la pestaña"
  - "en el centro"
items:
  - icon: 📁
    label: MiProyecto
    value: 0
  - icon: 📄
    label: OperacionSuma.cs
    value: 1
code: |-
  public class OperacionSuma
  {
      public int A { get; set; }
      public int B { get; set; }

      public int Sumar()
      {
          return A + B;
      }
  }
```

### 5. El inventario de nombres

#### Una clase con sentido

Ahora una clase con sentido: un inventario de nombres. Su dato principal es una lista de nombres, que es un atributo de la clase. Con ella podremos agregar nombres, modificarlos y traerlos todos.

```scene
id: oop-inventario
type: code
language: csharp
focus:
  - lines: [1]
    at: "Ahora una clase con sentido"
  - lines: [3]
    at: "una lista de nombres"
code: |-
  public class InventarioNombres
  {
      private List<string> nombres = new();
  }
```

#### El constructor

Un constructor es un código especial que prepara el objeto cuando lo creamos. Se llama igual que la clase, puede recibir datos y deja el objeto listo para usar. Aquí recibe el primer nombre y lo agrega a la lista.

```scene
id: oop-constructor
type: code
language: csharp
focus:
  - lines: [5, 6, 7, 8]
    at: "Un constructor es"
  - lines: [1, 5]
    at: "Se llama igual que la clase"
  - lines: [5]
    at: "puede recibir datos"
  - lines: [7]
    at: "Aquí recibe el primer nombre"
code: |-
  public class InventarioNombres
  {
      private List<string> nombres = new();

      public InventarioNombres(string primero)
      {
          nombres.Add(primero);
      }
  }
```

#### Los métodos

Un método es una acción que un objeto puede realizar. Nuestro inventario tiene tres: agregar un nombre, modificar uno existente y traer todos. Primero va public, luego lo que devuelve, después el nombre y los paréntesis. Dentro de las llaves está lo que hace.

```scene
id: oop-metodos
type: code
language: csharp
split: 14
focus:
  - lines: [10, 11, 12, 13]
    at: "Un método es una acción"
  - lines: [10]
    at: "agregar un nombre"
  - lines: [15]
    at: "modificar uno existente"
  - lines: [20]
    at: "traer todos"
  - lines: [20]
    at: "Primero va public"
  - lines: [21, 22, 23]
    at: "Dentro de las llaves"
code: |-
  public class InventarioNombres
  {
      private List<string> nombres = new();

      public InventarioNombres(string primero)
      {
          nombres.Add(primero);
      }

      public void Agregar(string nombre)
      {
          nombres.Add(nombre);
      }

      public void Modificar(int posicion, string nuevo)
      {
          nombres[posicion] = nuevo;
      }

      public List<string> TraerTodos()
      {
          return nombres;
      }
  }
```

#### Usar los objetos desde afuera

Desde fuera de la clase, creamos un objeto con new, que llama al constructor. Después usamos sus métodos con un punto: agregamos un nombre, modificamos otro y traemos todos. Como son public, podemos usarlos desde aquí. En cambio, la lista de nombres es private, así que queda oculta para el resto de la aplicación.

```scene
id: oop-use
type: code
language: csharp
focus:
  - lines: [1]
    at: "creamos un objeto con new"
  - lines: [2]
    at: "agregamos un nombre"
  - lines: [3]
    at: "modificamos otro"
  - lines: [4]
    at: "y traemos todos"
  - lines: [1, 2, 3, 4]
    at: "Como son public"
  - lines: [6]
    at: "es private"
code: |-
  var inventario = new InventarioNombres("Ana");
  inventario.Agregar("Luis");
  inventario.Modificar(0, "Ana María");
  var todos = inventario.TraerTodos();

  // inventario.nombres no se puede usar desde aquí: es private
```

### 6. Práctica: agrega un método para borrar

Ahora te toca a ti. Nuestro inventario puede agregar, modificar y traer nombres, pero todavía no puede borrar. Agrega un método llamado Borrar, que reciba la posición del nombre y lo quite de la lista. Las listas ya traen un método para eso: se llama RemoveAt. Escríbelo aquí mismo en el navegador y ejecuta las pruebas. Si quieres, después pídele a tu agente que lo pruebe también en un proyecto de consola.

```scene
id: practica-borrar
type: code
language: csharp
focus:
  - lines: [5]
    at: "Agrega un método llamado Borrar"
  - lines: [5]
    at: "que reciba la posición del nombre"
  - lines: [7]
    at: "Las listas ya traen un método"
code: |-
  public class InventarioNombres
  {
      // ... lo que ya tenemos

      public void Borrar(int posicion)
      {
          // tu código aquí
      }
  }
```

```exercise
id: practica-borrar-check
type: code-completion
language: csharp
prompt: "Completa el método Borrar para que quite el nombre de la posición indicada."
starter: |-
  public class InventarioNombres
  {
      private List<string> nombres = new();

      public InventarioNombres(string primero)
      {
          nombres.Add(primero);
      }

      public void Agregar(string nombre)
      {
          nombres.Add(nombre);
      }

      public void Modificar(int posicion, string nuevo)
      {
          nombres[posicion] = nuevo;
      }

      public List<string> TraerTodos()
      {
          return nombres;
      }

      public void Borrar(int posicion)
      {
          // tu código aquí
      }
  }
solution: |-
  public class InventarioNombres
  {
      private List<string> nombres = new();

      public InventarioNombres(string primero)
      {
          nombres.Add(primero);
      }

      public void Agregar(string nombre)
      {
          nombres.Add(nombre);
      }

      public void Modificar(int posicion, string nuevo)
      {
          nombres[posicion] = nuevo;
      }

      public List<string> TraerTodos()
      {
          return nombres;
      }

      public void Borrar(int posicion)
      {
          nombres.RemoveAt(posicion);
      }
  }
tests:
  - name: "Borrar quita el segundo nombre"
    expression: |-
      var inv = new InventarioNombres("Ana");
      inv.Agregar("José");
      inv.Agregar("Luis");
      inv.Borrar(1);
      Console.WriteLine(string.Join(", ", inv.TraerTodos()));
    expected: "Ana, Luis"
  - name: "Borrar el primer nombre"
    expression: |-
      var inv = new InventarioNombres("Ana");
      inv.Agregar("Luis");
      inv.Borrar(0);
      Console.WriteLine(string.Join(", ", inv.TraerTodos()));
    expected: "Luis"
explanation: "Una solución: nombres.RemoveAt(posicion);"
```

### 7. Un caso para pensar

Veamos un caso. Creamos el inventario con Ana. Agregamos a José y a Luis. Luego borramos el segundo nombre. Después modificamos el primero para que sea Carlos, y agregamos a Jesús. Al final, mostramos todos los nombres. Antes de seguir, piensa: ¿qué crees que va a salir? Elige tu respuesta.

```scene
id: caso-inventario
type: code
language: csharp
focus:
  - lines: [1]
    at: "Creamos el inventario con Ana"
  - lines: [2, 3]
    at: "Agregamos a José y a Luis"
  - lines: [4]
    at: "borramos el segundo nombre"
  - lines: [5]
    at: "modificamos el primero"
  - lines: [6]
    at: "agregamos a Jesús"
  - lines: [8]
    at: "mostramos todos los nombres"
code: |-
  var inventario = new InventarioNombres("Ana");
  inventario.Agregar("José");
  inventario.Agregar("Luis");
  inventario.Borrar(1);
  inventario.Modificar(0, "Carlos");
  inventario.Agregar("Jesús");

  Console.WriteLine(string.Join(", ", inventario.TraerTodos()));
```

```exercise
id: caso-inventario-salida
type: output-prediction
prompt: "¿Qué imprime este programa?"
choices:
  - "Carlos, Luis, Jesús"
  - "Carlos, José, Luis, Jesús"
  - "Ana, Luis, Jesús"
  - "Carlos, José, Jesús"
answer: 0
explanation: "Borrar(1) quita a José, el segundo nombre, porque las posiciones empiezan en cero. Luis pasa a la posición 1. Modificar(0, ...) cambia a Ana por Carlos, y Jesús se agrega al final."
```

### 8. ¿Qué ocurrió?

Veamos qué ocurrió, paso a paso. Al crear el inventario con Ana, la lista tiene un solo nombre. Agregamos a José y luego a Luis, y quedan tres. Borrar quita la posición uno. Recuerda que las posiciones empiezan en cero, así que el segundo nombre es José, y Luis pasa a ocupar la posición uno. Después modificamos la posición cero: Ana se convierte en Carlos. Agregamos a Jesús al final. Y al traer todos, vemos Carlos, Luis y Jesús.

```scene
id: caso-ejecucion
type: visual
visual: memory-list
items:
  - icon: 🆕
    label: 'new InventarioNombres("Ana")'
    detail: Crea el inventario
    at: "Al crear el inventario con Ana"
    steps: [Ana]
  - icon: ➕
    label: 'Agregar("José")'
    detail: Agrega a José
    at: "Agregamos a José"
    steps: [Ana, José]
  - icon: ➕
    label: 'Agregar("Luis")'
    detail: Agrega a Luis
    at: "y luego a Luis"
    steps: [Ana, José, Luis]
  - icon: 🗑️
    label: "Borrar(1)"
    detail: Quita la posición 1
    at: "Borrar quita la posición uno"
    steps: [Ana, Luis]
  - icon: ✏️
    label: 'Modificar(0, "Carlos")'
    detail: Cambia la posición 0
    at: "Después modificamos la posición cero"
    steps: [Carlos, Luis]
  - icon: ➕
    label: 'Agregar("Jesús")'
    detail: Agrega a Jesús al final
    at: "Agregamos a Jesús al final"
    steps: [Carlos, Luis, Jesús]
  - icon: 📥
    label: "TraerTodos()"
    detail: Devuelve la lista completa
    at: "Y al traer todos"
    steps: [Carlos, Luis, Jesús]
```

### 9. Errores: cuando algo sale mal

```exercise
id: errores-posicion
type: multiple-choice
prompt: "Si la lista tiene 3 nombres, ¿cuál es la última posición válida?"
choices:
  - "2"
  - "3"
  - "1"
answer: 0
explanation: "Las posiciones empiezan en cero: 0, 1 y 2."
```

```exercise
id: errores-validar
type: code-completion
language: csharp
prompt: "Valida Modificar y Borrar: si la posición no existe, no deben hacer nada ni fallar."
starter: |-
  public class InventarioNombres
  {
      private List<string> nombres = new();

      public InventarioNombres(string primero)
      {
          nombres.Add(primero);
      }

      public void Agregar(string nombre)
      {
          nombres.Add(nombre);
      }

      public void Modificar(int posicion, string nuevo)
      {
          nombres[posicion] = nuevo;
      }

      public List<string> TraerTodos()
      {
          return nombres;
      }

      public void Borrar(int posicion)
      {
          nombres.RemoveAt(posicion);
      }
  }
solution: |-
  public class InventarioNombres
  {
      private List<string> nombres = new();

      public InventarioNombres(string primero)
      {
          nombres.Add(primero);
      }

      public void Agregar(string nombre)
      {
          nombres.Add(nombre);
      }

      public void Modificar(int posicion, string nuevo)
      {
          if (posicion < 0 || posicion >= nombres.Count)
          {
              return;
          }

          nombres[posicion] = nuevo;
      }

      public List<string> TraerTodos()
      {
          return nombres;
      }

      public void Borrar(int posicion)
      {
          if (posicion < 0 || posicion >= nombres.Count)
          {
              return;
          }

          nombres.RemoveAt(posicion);
      }
  }
tests:
  - name: "Modificar fuera de la lista no falla"
    expression: |-
      var inv = new InventarioNombres("Ana");
      inv.Modificar(5, "Pedro");
      Console.WriteLine(string.Join(", ", inv.TraerTodos()));
    expected: "Ana"
  - name: "Modificar una posición válida sigue funcionando"
    expression: |-
      var inv = new InventarioNombres("Ana");
      inv.Modificar(0, "Carlos");
      Console.WriteLine(string.Join(", ", inv.TraerTodos()));
    expected: "Carlos"
  - name: "Borrar fuera de la lista no falla"
    expression: |-
      var inv = new InventarioNombres("Ana");
      inv.Borrar(9);
      Console.WriteLine(string.Join(", ", inv.TraerTodos()));
    expected: "Ana"
  - name: "Borrar una posición negativa no falla"
    expression: |-
      var inv = new InventarioNombres("Ana");
      inv.Borrar(-1);
      Console.WriteLine(string.Join(", ", inv.TraerTodos()));
    expected: "Ana"
explanation: "Comprueba que la posición exista (que no sea negativa y sea menor que la cantidad de nombres) antes de actuar."
```

#### El error

Un último tema: los errores. ¿Qué pasa si pedimos modificar la posición cinco, y la lista solo tiene tres nombres? Esa posición no existe, y el programa falla con un error. Los errores son normales, y es importante que nuestro código sepa evitarlos.

```scene
id: error-posicion
type: code
language: csharp
focus:
  - lines: [1]
    at: "Un último tema: los errores"
  - lines: [2]
    at: "modificar la posición cinco"
  - lines: [4, 5]
    at: "el programa falla con un error"
code: |-
  // La lista tiene 3 nombres: posiciones 0, 1 y 2
  inventario.Modificar(5, "Pedro");

  // Error: ArgumentOutOfRangeException
  // La posición 5 no existe
```

#### Validar antes de actuar

La solución es validar antes de actuar. Antes de modificar, comprobamos que la posición exista: que no sea negativa y que sea menor que la cantidad de nombres. Si no existe, el método simplemente no hace nada. Ahora te toca: en el ejercicio, agrega esa validación a Modificar y haz lo mismo con Borrar. Ejecuta las pruebas para comprobar que ya no fallan.

```scene
id: validar-posicion
type: code
language: csharp
focus:
  - lines: [3]
    at: "comprobamos que la posición exista"
  - lines: [5]
    at: "no hace nada"
code: |-
  public void Modificar(int posicion, string nuevo)
  {
      if (posicion < 0 || posicion >= nombres.Count)
      {
          return;
      }

      nombres[posicion] = nuevo;
  }
```

