# Convenciones

Debemos elegir alguna convención y ser estrictos con ella para mantener la coherencia del código y facilitar la escalabilidad y el mantenimiento futuro.

Lo siguiente no es más que una propuesta tras haber probado diferentes convenciones y haber visto sus consecuencias a largo plazo (buena o mala escalabilidad, mantenibilidad, bugs,...). Aunque algunos de estos consejos son muy básicos y comunes a cualquier convención, otros son opinables.

## Reglas de nomenclatura

### Estrictas:

- Todo lo que empiece por **mayúscula** es un **componente**
- Todo lo que empiece por **minúscula** es **otra cosa** (no componente)
- Un archivo o carpeta de **componente** sólo puede tener **un export default** (no hace export de nada más).
- Las **funciones** siempre empiezan por **verbo**
- Todo lo que no empiece por verbo (**sustantivo**, pronombre,...), será **otra cosa** (no es función):
    - Un componente
    - Conjunto de cosas: helpers, components, constants, contexts,...
    - Algo que necesite el proyecto: config, api, store, locales, auth,
- Los **hooks** siempre empiezan por **use**
- Los **HOCs** siempre empiezan por **with**

### Menos estrictas:

- Un archivo o carpeta que termine en **singular** tendrá sólo un export default
- Un archivo o carpeta que termine en **plural** tendrá varios exports
- Los **booleanos** deben tener un nombre que al leerlo, se infiera facilmente que contiene un true o false, para ello deben empezar por is, should, can, has, does,... y el resto puede ser indistintamente un adjetivo (isVisible), un nombre (isAdminUser, hasPermission), un verbo, etc... En caso de ser un verbo es preferible escribirlo en presente (ej: isOpen) ya que representan el estado actual de una variable, pero podemos hacer excepciones (ej: isAllowed, isLoaded,...).
- **Cuando un archivo** o carpeta **exporta una sola cosa** con export default, esa cosa que exporta **debe llamarse igual que el archivo** o carpeta.
- Todos los archivos, carpetas, funciones, variables y constantes modificables (arrays y objetos)... deben escribirse en **camelCase**
- Las **constantes** que no puedan ser modificadas (strings, booleans, freezed objects,...) deben escribirse en **mayúsculas y snake_case**.

### Evitar:

- **Nombres redundantes** (tanto en archivos y carpetas como en constantes y variables). Ejemplos:
    - Nombres de negocio: .../ComponentXx/~~ComponentXx~~Header.js
    - Nombres de tipo de archivo: .../helpers/doSomething~~Helper~~.js
- **Cambios de nombres** o alias al importar funciones, componentes, constantes, etc...
- **Acrónimos y abreviaturas**. No demos por hecho que quien venga detrás lo va a entender.

## Estructura de carpetas

- Todas las **carpetas** deben tener un **index.js** que exporte una o varias cosas, dependiendo de si el nombre de esa carpeta empieza por mayúscula o minúscula, es singular o plural, es verbo o sustantivo,...

- Cualquier cosa puede ser un **archivo** o una **carpeta**. Sólo depende del **tamaño** (en líneas de código) que tenga ese archivo.

    Ejemplo: Si tenemos un ComponenteX.js que contiene styled components, constantes, o algún hook o helper que sólo se usan en ese componente y hacen demasiado grande el archivo y queremos dividirlo, debemos crear una carpeta con el mismo nombre ComponenteX/ , mover el archivo ComponenteX.js a esa carpeta, renombrarlo a index.js y sacar los archivos que queramos a esa carpeta.
    
    <sub>Nota: Para hacer esto debemos parar y volver a ejecutar el bundler que tengamos levantado (webpack, parcel,...), de lo contrario, los imports darán un error de compilación.</sub>
    
- **Imports**: NUNCA importaremos nada de una ruta del interior de un componente. Es decir, esto estaría prohibido:
    ```javascript
    import { x } from "./ComponentXx/archivo"
    import { x } from "./ComponentXx/carpeta/loQueSea/..."
    ```

    Por ejemplo, si dentro de un ComponenteX tuviéramos un archivo o carpeta helpers con alguna función que quisiéramos usar fuera de ese componente, deberíamos mover esa función a un archivo/carpeta helpers superior (concretamente hasta nivel superior o componente “padre” de esos dos componentes que necesiten esa función.

    Los motivos de esta regla son principalmente dos:
    - Que en cualquier momento puedas cargarte un componente con todo lo que contenga y no se rompa nada fuera de él.
    - Evitar dependencias cíclicas. Si existen dependencias cruzadas de componentes que hacen lazy loading, webpack (o lo que usemos para hacer el bundle) tendría un problema con para hacer code splitting (chunks).

- Libertad total de nombres. Nos podemos inventar todos los nombres de archivos o carpetas tanto en mayúsculas (Componentes) como en minúsculas (otras cosas) que nos hagan falta.

    Ejemplos:\
    .../ComponentX/components/**filters**/... <small>(agrupando componentes que tienen algo en común)</small>\
    .../ComponentX/**units.js**

## [WIP] Moviéndonos por primera vez por un proyecto bien estructurado

Sin ver ni una sola línea de código, la estructura de carpetas de un proyecto puede ser suficiente para entender el proyecto. Veamos un ejemplo:

