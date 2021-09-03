# Buenas Prácticas

## URLs (Single source of truth)

- Que cuando recarguemos la página podamos llegar a ver la misma pantalla que estábamos viendo, a ser posible sin necesidad de usar local storage, cookies, etc,... para ello (casi) cualquier cambio en la interfaz (cambios de página a partir de menús/tabs principales, cambios de modo ver/editar, tipo de vistas tabla/lista/grid, ordenación y paginación de una tabla/lista principal,…) modifique la url (sea ruta o query params), exceptuando elementos triviales (tooltips, menus, dropdowns, expand/collapses, modales,...).
- Hacer uso de rutas relativas (reach-router). Las futuras versiones de react-router van por ese camino. Un componente que ha sido pintado como hijo de un router no tiene por qué saber cual es la ruta en la que está. Sólo las rutas relativas a partir de él.
- Hacer más uso de links y menos abuso de onClicks. Los links ayudan a la navegación (poder volver atrás, abrir en pestaña nueva,...)
- Búsquedas y filtros que sólo modifican query params. No duplicar estados.

## html semántico

- Usar menos div/span y más los tags de layout con más semántica: header, main, footer, aside, section, article, nav,...
- Evitar meter textos directamente dentro de tags de layout. El texto siempre debe estar dentro de tags de formulario (button, inputs,...) o de texto (p, headings, a, blockquote,...) que a su vez pueden tener tags específicos según las necesidades (em, strong, span, mark, sub, sup...).
- Cuando queramos hacer tablas, usar los tags para hacer tablas. Las tablas se adaptan automáticamente al contenido, podemos hacer columnas de anchos fijos, mínimos, máximos, scroll horizontal,...

## Pensar de forma declarativa y funcional (React)

- No usar NUNCA programación imperativa a menos que sea estrictamente necesario (ej: un focus de un input, un botón que hace un refetch,...). React es declarativo y debemos pensar de forma declarativa.

- Un componente de react es una función (vale sí, también existen las clases, pero podemos ignorarlas desde que aparecieron los hooks). Las props no son más que los argumentos de esa función. Por lo tanto, podemos hacer uso del paradigma de programación funcional estricto y del concepto de función pura para aprovechar sus ventajas y hacer componentes sencillos, con poca responsabilidad, testeables, sin efectos colaterales, etc,.... y de la misma forma, extraer de esos componentes más funciones puras, componentes, helpers y custom hooks que unifiquen lógica duplicada entre distintos componentes.
