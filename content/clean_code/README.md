# Resumen por secciones
# 1 Código limpio (introducción)
Poner etiqueta `@author` en javadoc (para que los demás sepan quién lo escribió).

Sólo se escribe código el 10% del tiempo (10:1). El otro 90% se pasa leyendo código anterior, cambiando entre módulos, etc.

**Regla del Boy Scout**: entregar el código más limpio de lo que lo hemos recibido.

# 2 Nombres con sentido

## 2.1 Nombres que revelen las intenciones
Prestar atención a los nombres y cambiarlos cuando se encuentren otros mejores.
Si un nombre requiere un comentario, es que no revela su cometido.

Ejemplos de tiempo: `elapsedTimeInDays`, `daysSinceCreation`.

Usar constantes/enums para valores y subíndices.
No usar nombres que puedan significar otra cosa y confundir. Ej: `hp` puede ser hipotenusa o una plataforma de linux.

Usar sufijos `-list`, `-map`, etc cuando realmente sean cosas de ese tipo. En caso contrario: `bunchOf-`, `-Group` o simplemente el nombre sin prefijo ni sufijo.

Evitar variaciones mínimas: dos nombres casi iguales en el mismo contexto, sobre todo en nombres largos.

Evitar _l_ y _O_ por su similitud a _1_ y _0_.


## 2.2 Distinciones entre nombres

Usar nombres distintos si tienen significados diferentes. Ejemplo a evitar: `a1`, `a2`, …, `aN` como nombres de parámetros.

Evitar palabras adicionales para distinguir entre nombres. Ej: `product` vs `productInfo`, `-info`, `-Data`, `a-`, `an-`, `the-`.

Evitar palabras redundantes. Ej: `variable` u `object` en el nombre de una variable, `nameString` (porque siempre `name` es un string).

## 2.3 Que se puedan pronunciar
Evitar siglas impronunciables: `genymdhms` (_gen year-month-day-hour-minute-second_)

## 2.4 Que se puedan buscar
Si se va a usar en varios ámbitos, hay que evitar usar directamente los números de constantes (sustituir por nombres) o nombres de pocas letras. Excepción: si es de uso local.

## 2.5 Evitar nombres codificados
Evitar usar abreviaturas, prefijos, sufijos con significado no estándar.

### 2.5.1 Evitar notación húngara (HN)
Antiguamente se ponía el tipo de la variable en el nombre. Ej: `phoneString`.
El nombre no cambia automáticamente cuando cambia el tipo.

### 2.5.2 Evitar prefijos de miembros
Antiguamente se ponía `m_` antes de una variable miembro de una clase.

### 2.5.3 Interfaces e implementaciones
No explicitar en el en nombre de Interfaces que sea una interfaz (añadir una `I-` inicial, `-Interface`, etc.).

En implementaciones sí se usa `-Imp` o `C-`. Ej: `ShapeFactory`(interface) -> `ShapeFactoryImp` / `CShapeFactory`

## 2.6 Evitar asignaciones mentales
En contadores de bucles pequeños se puede usar `i`, `j`, `k`. Para usos más concretos, mejor usar un nombre normal.

## 2.7 Nombres de clases
Evitar palabras dentro del nombre de una clase (como prefijo, sufijo o interfijo):
* `Manager`,
* `Processor`,
* `Data`,
* `Info`.

No usar verbos.

## 2.8 Nombres de métodos
Verbo.

Usar `get-`/`set-`/`is-` como el estándar javabean.

Si se necesita sobrecargar el constructor, usar métodos de factoría estáticos, con un nombre que describa los argumentos. Ej: `Complex.fromRealNumber(23.0)`

Convertir en privados sus constructores correspondientes (para obligar a usar los métodos de factoría).

## 2.9 Evitar expresiones coloquiales
Ej: `eatMyShorts()` en vez de `abort()`.

## 2.10 Una palabra por concepto
Evitar palabras diferentes para el mismo concepto en clases diferentes. Usar una y mantenerla en todas las clases. Ej: `fetch-`, `retrieve-` y `get-`.

Evitar clases con nombre conceptualmente equivalentes en la misma base de código. Ej: `DeviceManager` vs `ProtocolController`.

## 2.11 Diferente concepto, diferente palabra
Evitar usar la misma palabra para fines distintos (suele pasar cuando son similares). Ej: `add` vs `insert` vs `append`.

## 2.12 Usar nombres técnicos
Usar nombres técnicos de ámbito informático, matemático, algorítmica, etc.
Ej: `AccountVisitor` usa el patrón VISITOR.

[Relacionado con 2.10]

## 2.13 Usar nombres de dominios de problemas
Si no hay nombre técnico de programación [2.12], usar nombre técnico de su ámbito.

## 2.14 Añadir contexto con sentido
Los nombres suelen tener significado según su contexto (en una función, en una clase…).

En métodos largos (o con cosas que parezca obligado comentar por lo que significa por ejemplo un `if..else`), conviene separarlos y añadirlos a una clase como contexto.

Si no se puede añadir un contexto, añadir prefijos de contexto al nombre.

## 2.15 No añadir contextos innecesarios
No añadir prefijos/sufijos/interfijos de contexto si ya está contextualizado el nombre. Ej: no llamar a una clase `GSDAccountAddress` si está dentro de la aplicación `GSD` y del módulo `MailingAddress`.

# 3 Funciones

## 3.1 Tamaño reducido
Unas **20 líneas** si no pueden reducirse más los niveles de abstracción.

Cada línea de **150 carácteres** como máximo.

### 3.1.1 Bloques y sangrado
Las funciones `if`, `else` y `while` deben tener cuerpo de sólo una línea.

## 3.2 Hacer una cosa
Las funciones sólo deben hacer una cosa.

_una cosa_: los niveles de abstracción inmediatamente inferiores al nombre de la función.

### 3.2.1 Secciones en funciones
Síntoma de que hace más de una cosa.

## 3.3 Un nivel de abstracción por función
Evitar mezclar distintos niveles de abstracción. (Subcaso de [3.2])

### 3.3.1 Leer código de arriba a abajo: la regla descendente
Comprobación de [3.3]

## 3.4 Instrucciones `Switch`
Ocultarlas con una factoría abstracta y usar el patrón visitor. Así sólo se usará una vez el `switch` (al crear la instancia) y no será visible.

## 3.5 Usar nombres descriptivos
Cuanto más concreta y sencilla sea una función, más fácil será elegir el nombre.

Mejor extenso y descriptivo que breve y enigmático.

## 3.6 Argumentos de funciones
Los argumentos dificultan la lectura y obligan a conocer más el contexto y los niveles de abstracción hacia abajo.

Usar el menor número de argumentos posible; como **máximo 2** (salvo caso justificado).

Si hay pocos argumentos, se facilita hacer las pruebas (hay menos casos que probar).

### 3.6.1 Formas monádicas habituales
Usos de funciones con sólo un argumento:
* Pregunta sobre el argumento. Ej: `boolean fileExists(“MyFile”)`.
* Transforma el argumento en otra cosa y la devuelve. Ej: `InputStream fileOpen(“MyFile”)`
* Eventos que cambian el estado del sistema. Ej: `void passwordAttemptFailedNtimes(int attempts)`.

### 3.6.2 Argumentos de indicador
Evitar usar argumentos boolean.

### 3.6.3 Funciones diádicas
A veces es confuso saber cuál es la diferencia entre el primer y segundo parámetro (sobre todo si son del mismo tipo). Ej: `assertEquals(x, y)` (cuál es el esperado y cuál el real?)
Convertir en monádicas si se puede.

### 3.6.4 Triadas
Desaconsejado, salvo caso justificado.

Ejemplo de caso justificado: comparaciones de float. Ej: `assertEquals(1.0, amount, .001)`

### 3.6.5 Objeto de argumento
Si se pasan muchos argumentos, quizá se puede hacer una abstracción. Ej: `makeCircle(x, y, radius)` -> `makeCircle(Point center, radius)`

### 3.6.6 Listas de argumentos
Los argumentos variables (`Object… args`) cuentan (en las reglas anteriores) como uno solo de tipo List

### 3.6.7 Verbos y palabras clave
Monádicas: verbo (describe a la función en general) y sustantivo (describe al argumento). Ej: `writeField(name)`

## 3.7 Sin efectos secundarios
Si no se puede evitar que una función haga sólo una cosa, hay que reflejarlo en el nombre. Ej: `checkPasswordAndInitializeSession` en vez de sólo `checkPassword`.

### 3.7.1 Argumentos de salida
Antes de _OOP_ tenían sentido.

Evitar.

## 3.8 Separación de consultas de comando
Una función puede cambiar el estado u obtener el estado, pero nunca ambas cosas a la vez.

## 3.9 Mejor excepciones que devolver códigos de error
Con códigos de error se generan estructuras anidadas y el mismo invocador debe procesar el error. Con excepciones se separa el invocador del procesador del error y se evita la estructura anidada.

### 3.9.1 Extraer bloques `try..catch`
Extraer el cuerpo de las funciones `try` y `catch` (respectivamente) a dos funciones individuales.

### 3.9.2 El procesamiento de errores es una cosa
No debe haber nada más después de cerrar el `try..catch` ni antes.

### 3.9.3 El imán de dependencias Error.java
Si creamos un enumerado con errores, no se pueden añadir/cambiar sin recompilar todo el código que depende de ello. Mejor usar excepciones (la clase Exception siempre está).

## 3.10 No repetirse
Evitar código duplicado (si hay que cambiar algo, habría que cambiarlo en todos los sitios).

## 3.11 Programación estructurada
En funciones pequeñas no tiene sentido usar las reglas de Dijkstra (sólo un `return`, evitar `break`/`continue` y el `goto`). Aunque el `goto` sólo tendría sentido en funciones grandes y se tiene que evitar.

## 3.12 Cómo crear este tipo de funciones
Las reglas de funciones no se aplican directamente a la primer al escribir el código. Primero se escribe y luego se refactoriza.

# 4 Comentarios

## 4.1 Los comentarios no compensan el código incorrecto, 4.1.1 Explicarse en el código, 4.2.2 Comentarios informativos
Se tienen que evitar comentarios si, aplicando las reglas de Clean Code, no son necesarios.

## 4.2 Comentarios de calidad
[]

### 4.2.1 Comentarios legales
Hacer referencias a documentos externos en vez de incluir todos los términos.

### 4.2.3 Explicar la intención
Los comentarios están justificados para informar de una decisión. Ej: al ordenar una lista de objetos, poner por encima los de una clase determinada porque el programador considera que son los correctos.

### 4.2.4 Clarificación
Cuando se usa una librería estándar o código que no se puede modificar. Ej: los valores devueltos de `obj.compareTo(obj2)`.
Riesgo: que los comentarios sean incorrectos.

### 4.2.5 Advertir de las consecuencias
Ej: “no ejecutar si no se tiene tiempo porque es lento”

### 4.2.6 Comentarios `TODO`
Permitidos. Cosas a hacer en el futuro.

### 4.2.7 Amplificación
Indicar la importancia y por qué de una parte del código.

### 4.2.8 Javadoc en API públicas
Si se crea una API pública, hay que hacer un javadoc.

## 4.3 Comentarios incorrectos, 4.3.1 Balbucear, 4.3.2 Comentarios redundantes, 4.3.3Comentarios confusos
[]
### 4.3.4 Comentarios obligatorios
No poner javadoc o comentario a todas las variables sistemáticamente. Muchas veces es redundante y complican la lectura.

### 4.3.5 Comentarios periódicos
Evitar comentarios de tipo changelog.

### 4.3.6 Comentarios sobrantes
Igual que [4.3.2]

### 4.3.7 Comentarios sobrantes espeluznantes
Si hay que usar copy paste en comentarios, seguramente sean redundantes.

### 4.3.8 No usar comentarios si se puede usar una función o variable
Refactorizar expresiones complicadas usando variables.

### 4.3.9 Marcadores de posición
Evitar comentarios que dividan por secciones el código, salvo que sea algo particular de la clase. Ejemplo: “Acciones”, “Getters”

### 4.3.10 Comentarios de llave de cierre
No tienen sentido en funciones cortas.

### 4.3.11 Asignaciones y menciones
No poner comentarios como _añadido por X_, eso se hace en el sistema de control de código fuente.

### 4.3.12 Código comentado
No dejar código comentado.

### 4.3.13 Comentarios HTML
Evitar. Dificulta la lectura.

### 4.3.14 Información no local
No comentar cosas que hagan referencia a otras partes del código (pueden ser cambiadas).

### 4.3.15 Demasiada información
Evitar explicar protocolos, información teórica, etc.

### 4.3.16 Conexiones no evidentes
Tiene que quedar claro la relación entre los elementos generales del comentario y los particulares de la implementación.

### 4.3.17 Encabezados de función
Evitar. Una función con buen nombre no los necesita.

### 4.3.18 Javadocs en código no público
Evitar.

# 5 formato
## 5.1 La función del formato
[]
## 5.2 Formato vertical
Archivos normales **200-500 líneas**. Los archivos de pequeño tamaño se entienden mejor.

### 5.2.1 La metáfora del periódico
Arriba lo más importante.

### 5.2.2 Apertura vertical entre conceptos
Usar línea en blanco para separar conceptos: Ej: línea en blanco tras los imports, entre funciones, etc.

### 5.2.3 Densidad vertical
Si dos o más líneas van seguidas, se consideran relacionadas.

### 5.2.4 Distancia vertical
Los conceptos relacionados entre sí deben mantenerse juntos verticalmente.

#### 5.2.4.1 Declaraciones de variables (en funciones)
Deben declararse de la forma más cercana a su uso (lo más tarde posible y en el bloque más interno posible).

#### 5.2.4.2 Variables de instancia (clase)
Java: parte superior.
C++: parte inferior.

#### 5.2.4.3 Funciones dependientes
Si una función invoca a otra deben estar verticalmente próximas, y la invocadora siempre arriba de las invocadas (siempre que sea posible).

#### 5.2.4.4 Afinidad conceptual
Las cosas afines deben estar próximas.

### 5.2.5 Orden vertical
Como [5.2.1] y [5.2.4.3].

## 5.3 Formato horizontal
Máximo **80-120 carácteres por línea**.

### 5.3.1 Apertura y densidad horizontal
Espacio en operadores binarios (excepto en multiplicaciones o divisiones internas).

### 5.3.2 Alineación horizontal
No usar tabulado para separar tipos, nombres de variables, etc.

### 5.3.3 Sangrado
Para jerarquía.

#### 5.3.3.1 Romper el sangrado
Evitar romper el sangrado haciendo ámbitos de una línea Ej: constructores que declaran un constructor llaman a `super()` y cierran la función en una misma línea, funciones que sólo tienen un `return` y se hace en la misma línea.

### 5.3.4 Ámbitos ficticios
Bucles sin cuerpo, poner punto y coma en la línea siguiente con sangrado.

### 5.3.5 Reglas de equipo
Usar las reglas de formato que decida el equipo.

# 6 Objetos y estructuras de datos
## 6.1 Abstracción de datos
Usar interfaces. No mostrar detalles de na implementación ni de los datos (no poner cosas tipo `getInMeters()`, sino `getLength()` ).

## 6.2 Antisimetría de datos y objetos
* Datos: _point_, _rectangle_, _circule_…
* Objetos: comportamiento (funciones) de los datos.

* Datos y objetos juntos: programación orientada a objetos (_OOP_, _**O**bject-**o**riented **P**rogramming_).
* Datos y objetos separados: programación orientada a procedimientos (_POP_, **P**rocedure-**o**riented **P**rogramming).

Al añadir nuevas funciones:
* _POP_: se modifica solo el objeto (poniendo un `switch` según el tipo de dato en la nueva función)
* _OOP_: hay que cambiar todas las clases de datos usando polimorfismo.

Al añadir nuevos tipos de datos:
* _POP_: hay que cambiar todas las funciones para añadir qué hacer en caso de los nuevos tipo de datos.
* _OOP_: se implementan las funciones en el nuevo tipo sin modificar el resto de funciones.

## 6.3 La ley de Demeter
Un módulo debe ocultar su estructura interna. Cada módulo sólo tendrá acceso a la estructura interna de sus unidades más cercanas e imprescindibles.

En términos técnicos: un método `f` de la clase `C` sólo debe llamar a las funciones de:
* `C`
* Un objeto creado por `f`
* Un objeto pasado como argumento por `f`
* Un objeto de una variable de instancia de `C`

### 6.3.1 Choque de trenes
Evitar cosas tipo: `String dir = ctx.getOptions().getDir().getAbsolutePath()`
Separar caca objeto devuelto.
Excepto si son datos (y no objetos), ya que la ley de Demeter no se incumpliría, ya que no muestran detalles de implementación.

### 6.3.2 Híbridos
Si no se cumple la ley de Demeter, la clase tendrá variables y funciones que deberían ser privadas. Esto dificulta añadir nuevas funciones y estructuras de datos (tiene lo peor de ambos mundos).

### 6.3.3 Ocultar la estructura
[]

## 6.4 Data Transfer Object (DTO)
Clases con todos los métodos públicos. También los beans, pero no tienen ninguna ventaja real.
Usados normalmente como primer paso en la conversión de datos sin procesar. Ej: comunicación con BDs, analizar mensajes de conexiones, etc.

### 6.4.1 Active Record
Forma especial de _DTO_. Tiene métodos de navegación (`save`, `find`…). Suelen ser traducciones directas de tablas de BD u otros orígenes de datos.
No añadirles más métodos, ya que se convertiría en un híbrido [6.3.2]. Si hay que describir la forma de incorporar estos datos al programa (reglas empresariales), crear objeto independiente que use estos datos (así se ocultan los datos internos).

# 7 Procesar errores
## 7.1 Usar excepciones en lugar de códigos devueltos
Antes era mediante códigos: el invocador debe comprobar los errores tras la invocación y se suele olvidar. Por ello, mejor con excepciones. Además el código es más limpio: se separa el invocador del control de errores.

## 7.2 Crea primero la instrucción `try..catch..finally`
Hacer las comprobaciones `try..catch` lo antes posible en el código.

## 7.3 Usar Unchecked Exceptions
Unchecked Exception (no comprobadas por el compilador): usar siempre try-catch, nunca throws en las funciones (porque esto rompería la encapsulación y propaga los cambios en cascada). Excepción: librerías.

## 7.4 Ofrecer contexto junto a las excepciones
Mensajes de error: indicar la operación fallida y el tipo de fallo.

## 7.5 Definir clases de excepción de acuerdo a las necesidades del invocador
Crear wrappers sobre funciones de librería que lancen excepciones (sobre todo cuando lanzan muchas excepciones) capturando las excepciones y tratándolas (incluso haciendo que lance excepciones creadas por nosotros)

En general (no sólo para excepciones), es una buena práctica utilizar wrappers sobre librerías de terceros: se minimizan las dependencias y permite cambiar de librería en el futuro sin modificar mucho código.

## 7.6 Definir el flujo normal
Usar clases para procesar los casos especiales mediante polimorfismo (patrón Fowler, parecido a Visitor).

## 7.7 No devolver `null`
Devolver en su lugar valores vacíos; así se evitan las comprobaciones de null. Ej: `Collections.emptyList()`

## 7.8 No pasar `null`
No pasar `null` como parámetro intencionalmente. Así, un null como argumento nos indicará que algo falla.

# 8 Límites
Límites: API pública de código de terceros.

## 8.1 Utilizar código de terceros
El código de terceros suele ser genérico, multipropósito; a veces es un inconveniente cuando se quieren restringir algunas cosas. Ej: que un map no se pueda borrar (pero tiene el método `clear`).

Evitar usar interfaces como `Map` como argumento o valor de retorno en una API pública, mantenerlas dentro de otra clase.
## 8.2 Explorar y aprender límites
Hacer pruebas de aprendizaje cuando utilizamos código de terceros, en vez de usarlo directamente sobre el código de producción.
## 8.3 Aprender log4j
Aprender log4j y encapsularlo en nuestra propia clase de _logging_.
## 8.4 Las pruebas de aprendizaje son algo más que gratuitas
También sirven para comprobar que el código sigue funcionando como esperamos cuando se cambia de versión de código de terceros.Sin las pruebas, es probable que mantengamos una versión antigua pensando que no sería compatible con nuestro código cuando sí lo es.
## 8.5 Usar código que todavía no existe
Crear primero interfaces. 
[no entendido. buscar sobre adapter pattern y seam]
## 8.6 Límites limpios
No depender de código de terceros. Usar un _wrapper_ [8.1] o un _adapter_ [8.5].

# 9 Pruebas unitarias
## 9.1 Las tres leyes del DGP
Escribir primero las pruebas que el código de producción

1. No crear código de producción hasta que una prueba unitaria falle.
1. No escribir más tests unitarios que el necesario para que falle (que no compile se considera como fallo).
1. No crear más código de producción que el necesario para superar la prueba de fallo actual.

Estas tres leyes generan un ciclo de 30 segundos. Las pruebas y el código de producción se crean de forma conjunta (primero las pruebas y unos segundos después el código).
## 9.2 Realizar pruebas limpias
El código de prueba es tan importante como el de producción y requiere ser igual de limpio.
### 9.2.1 Las pruebas proporcionan posibilidades
Si hay pruebas, no habrá miedo a realizar cambios en el código; porque sin pruebas, cada cambio es un posible error. Por tanto, hacen que el código de producción sea flexible.
## 9.3 Pruebas limpias
Se usan las mismas reglas de código limpio en las pruebas.
### 9.3.1 Lenguaje de pruebas específico del dominio
Conforme se van haciendo varias pruebas y se va refactorizando el código, surge un _lenguaje de pruebas específico_ que facilita la lectura.
### 9.3.2 Un estándar dual
En entornos de prueba se puede no ser tan eficiente como en producción. Ej: concatenar _strings_ con el operador suma en vez de con `StringBuffer`.
## 9.4 Una afirmación (assert) por prueba
Intentar usar el menor número de _assert_ en los tests (idealmente sólo uno)
### 9.4.1 Un solo concepto por prueba
Un solo concepto por prueba.
## 9.5 F.I.R.S.T.
* (_**F**ast_)Rapidez: deben ejecutarse rápidamente (si no, no se ejecutarán con frecuencia)
* (_**I**ndependent_)Independencia: no deben depender entre ellas (dificultaría diagnóstico y ocultaría errores posteriores).
* (_Repeteable_)Repetición: deben poder hacerse en cualquier entorno.
* (_**S**elf-Validating_)Validación automática: las pruebas deben tener un resultado booleano (aciertan o fallan) (si no, en resultado puede ser subjetivo y la comprobación, manual).
* (_**T**imely_)Puntualidad: crearlas antes del código de producción (si no, puede parecer demasiado difícil de hacer las pruebas y no hacerlas).

# 10 Clases
## 10.1 Organización de clases
1. Variables: constantes estáticas públicas, estáticas privadas, privadas.
1. Funciones públicas (incluimos las utilidades públicas invocadas por una función tras la propia función).
### 10.1.1 Encapsulación
Si las variables son protected (no ponerlas así por esta razón), se pueden invocar desde las pruebas.
## 10.2 Las clases deben ser de tamaño reducido
Al igual que las funciones, tienen que ser lo más reducidas posible. La medida de tamaño en las funciones era las líneas, en las clases serán las responsabilidades (evitar _clase Dios_). No hay una relación directa entre la cantidad de funciones y de responsabilidades de una clase.
Usar nombres largos o ambiguos suele ser indicador de muchas responsabilidades.
Poner una descripción de la clase de unas 25 palabras (evitar: _si_, _y_, _o_, _pero_; suele ser indicador de demasiadas responsabilidades).
### 10.2.1 El principio de responsabilidad única (_SRP_)
Responsabilidad: razón que tiene la clase para cambiar en el futuro.

Mejor tener muchas clases con una responsabilidad que una con muchas.
### 10.2.2 Cohesión
Una clase en la que todas las variables de instancia se usa en todos los métodos tiene una cohesión máxima. Se intentará que la cohesión sea lo más alta posible.

Si al refactorizar se crean muchas nuevas variables instancia, suele ser indicador de que hay que separar en dos o más clases.
### 10.2.3 Mantener resultados consistentes en muchas clases de tamaño reducido
- (Ejemplo de separación de clases al refactorizar).

## 10.3 Organizar los cambios
Si cambiamos una clase que incumple _SRP_, hay que corregir su diseño.
### 10.3.1 Aislarnos de los cambios
Usar interfaces y clases abstractas (que representan conceptos) para aislar los detalles concretos, para que cuando éstos cambien no afecten a los conceptos. Así también se cumple el Principio de Inversión de Dependencias (_DIP_).

# 11 Sistemas
## 11.1 Cómo construir una ciudad
Se necesita a mucha gente. Algunos se encargan de aspectos generales y otros se centran en los detalles.
## 11.2 Separar la construcción de un sistema de uso
Evitar técnica de inicialización/evaluación tardía (se crean dependencias, incumple _SRP_).

Modularizar este proceso:
### 11.2.1 Separar `Main`
Trasladar todos los aspectos de construcción a main. Así, la aplicación no tiene conocimiento de `main`: se oculta en proceso de inicialización.
### 11.2.2 Factorías
Usar factoría abstracta cuando la aplicación sea responsable de crear objetos.
### 11.2.3 Inyectar dependencias
Inversión de control (_IoC_): pasa responsabilidades secundarias de un objeto a otros más específicos.
En inyección de dependencias, se debe delegar a otro objeto la instanciación de dependencias. La información para inyectar estas dependencias suele estar en la configuración global. Ej: en Spring mediante archivos de configuración XML.
## 11.3 Evolucionar
No se pueden conseguir sistemas perfectos a la primera (porque cambian las necesidades).
### 11.3.1 Aspectos transversales
Usar capa de persistencia para que las modificaciones de comportamiento no sean invasivas en el código de destino.
## 11.4 Proxies de Java
Los proxies JDK utilizan mucho código hasta para casos sencillos. Dificulta la creación de código limpio. No ofrecen un mecanismo para especificar puntos de ejecución globales del sistema (los AOP, sí).

POJO: Plain-Old Java Object (objeto sencillo de Java)

## 11.5 Estructuras AOP Java puras
Usadas en Spring AOP y JBoss AOP.

DAO: Data Accessor Object (objeto de acceso de datos).

### 11.5.1 Aspectos de AspectJ
AOP sirve para el 80-90% de los casos. Para casos más avanzados: AspectJ.

## 11.6 Pruebas de unidad de la arquitectura del sistema
Una arquitectura de sistema óptima se compone de dominios de aspectos modularizados, cada uno con POJO. Los dominios se integran mediante aspectos/herramientas similares mínimamente invasivas. Se le pueden realizar pruebas igual que en el código.

## 11.7 Optimizar la toma de decisiones
Posponer las decisiones hasta el último momento: para tener más información.

## 11.8 Usar estándares cuando añadan un valor demostrable
Usar estándares (reutilización, más fácil que hayan expertos, etc.), pero tampoco obsesionarse. No hay que perder de vista el objetivo.

## 11.9 Los sistemas necesitan lenguajes específicos del dominio (DSL)
DSL: Domain-Specific Languages.
Lenguajes de programación o modelado específicos de un dominio. Permite expresar todos los niveles de abstracción de un dominio.
Dirigidos a expertos en el dominio.

Son todo lo contrario a lenguajes de programación (C++/Java) o de modelado (UML) de carácter general 

Ej: Game Maker Language (GML), UnrealScripts.

# 12 Emergencia
## 12.1 Limpieza a través de diseños emergentes
Reglas de Kent Bleck de diseño sencillo:
* Ejecutar todas las pruebas.
* No contener duplicados.
* Expresar la intención del programador.
* Minimizar el número de clases y métodos.

Facilita aplicar principios _SRP_ y _DIP_.

## 12.2 Primera regla del diseño sencillo: Ejecutar todas las pruebas.
Todo diseño necesita una forma sencilla de comprobar que realmente funciona: sistema testable. Por tanto, la creación de pruebas conduce a obtener mejores diseños.

## 12.3 Reglas 2 a 4 del diseño sencillo: Refactorizar
Tras crear las pruebas, refactorizamos. Volvemos a ejecutar las pruebas con frecuencia al limpiar el código.
Dentro de la refactorización:
* Aumentar la cohesión.
* Recucir las conexiones.
* Separar las preocupaciones.
* Modularizar aspectos del sistema.
* Reducir el tamaño de funciones y clases.
* Elegir nombres adecuados.
* Eliminar duplicados [12.4].
* Garantizar la capacidad de expresión [12.5].
* Minimizar el número de clases y métodos [12.6].
## 12.4 Eliminar duplicados
Eliminar código duplicado (aumentar dependencia de funciones del programa). Ej: hacer que `isEmpty()` dependa de `size()`.

## 12.5 Expresividad
Al aumentar la complejidad del sistema, el programador necesita más tiempo para entenderlo y aumentan las posibilidades de error.

Elegir nombres adecuados, reducir tamaño de funciones y clases, usar nomenclatura estándar (ej: añadir nombre de patrón estádar como `-Command` o `-Visitor` en clases que implementan dichos patrones). Las pruebas también ayudan a entender lo que hace una clase.

## 12.6 Clases y métodos mínimos
Reducir el número de clases y métodos, siempre que no entre en conflicto con las reglas anteriores (evitar llevarlas al extremo).

# 13 Concurrencia
