# Licencia
- URL licencia (MIT): https://opensource.org/licenses/MIT
- readme.MD:
# guerrerosZ
```
Es un juego realizado en JS utilizando de momento un único fichero HTML 
donde se incluyen los estilos, la semántica HTML y el script JS dentro 
del tag, todo dentro del fichero HTML.
```
## Descripción del Refactor realizado
-	Librerías y cargues CDN: se carga de momento JQuery en la cabecera del HTML (CDN) para recorrer la lista de tablas generadas en el JS.
-	JS: se agrega cierta funcionalidad para dejar la lógica lo más modular posible. Esto con el objetivo de implementar el patrón de diseño REVELADOR, 
que no es más que envolver todo el flujo principal de ejecución del programa  (BATALLA) en una única función para tener control (Acceso) a sus miembros.
Esto representa un SCOPE, y es parte del principio del desarrollo en Angular JS.


## Propuesta a los compañeros del curso de fundamentos:
- Propongo básicamente, que cada estudiante descargue normal el repositorio y ver el funcionamiento en sus entornos locales, pero aparte de esto, que mantengamos esta versión base para realizar aportes de ideas que surgan en cada capa, es decir, a X compañero se le ocurrio una mejora a nivel de CSS, y al compañero Y, se le ocurrio mejorar la lógica del juego en la función Javascript. Con esta versión base se pretende mejorar la aplicación para fines académicos y reforzar fundamentos.
- La idea es simular un entorno real de desarrollo, donde cada aporte (Pull Request) será bienvenido y mejoraremos notablemente este juego hasta llegar a ser multiplataforma. Todo partiendo de la solución a los requerimientos iniciales planteados en la lista correspondiente.

- Se intentará Llevar el historial de asignación de tareas actuales en el localStorage del servidor (Github pages) u otro medio propuesto por un estudiante.
- Establecer/proponer un flujo de trabajo solido y fluido para realizar tareas de despliegue de manera sencilla, y cada integrante pueda aportar al proyecto base.



## Requerimientos INICIALES (CSS, HTML, JS):
- A continuación está la propuesta de requerimientos BASE, la idea es que quien postule a este proyecto escoja un requerimiento para trabajar en su entorno local mientras realiza todo el procedimiento explicado en el curso profesional de GITHUB para interactuar con repositorios y proponer una mejora o aporte al proyecto.

- Listado de requerimientos propuestos:
- [REQ-01]: Separar del HTML actúal "index.html" en un fichero aparte todo el código CSS.
- [REQ-02]: Una vez separados los ficheros, se requiere que el todo CSS sea adaptativo y RESPONSIVE, es decir, desplegar el Juego en todas las resoluciones de pantalla, 
incluyendo Tablets, iPad (PRO y NORMAL), Tablets pequeñas, iPhone 5 y 6.  Conforme se detalle la visualización de los elementos en la pantalla.
- [REQ-02-01]: Agregar una tipografía estable y equilibrada para la buena lectura.
- [REQ-03]: Separar del HTML actúal "index.html" en un fichero aparte con todo el códifo JAVASCRIPT.
- [REQ-04]: Agregar audio mientras se están desplegando las imagenes que son la secuencia de la batalla.
- [REQ-05]:Agregar a nivel de maquetación, un panel en la izquierda que representa más detalles sobre la BATALLA.
- [REQ-06-SR]: Implementar Servicios y Frontend para  consumir desde un cliente la Batalla (ANDROID, IOS).
- [REQ-05-01]: Modificar el mecanismo de escritura sobre el DOM, reemplazando el .write por .append( ... )
- [REQ-07-JR]: Configurar etiquetas/directivas en el <head> del documento.



- El proceso de asignación de los requerimientos/Tareas, se estará planeando conforme a sus propuestas, opiniones y de más.


## Créditos
- [Twitter Iván Darío](https://twitter.com/cosmosoftroot)
- [Twitter Jaime Iván Diaz](https://twitter.com/jdiaz0017)
