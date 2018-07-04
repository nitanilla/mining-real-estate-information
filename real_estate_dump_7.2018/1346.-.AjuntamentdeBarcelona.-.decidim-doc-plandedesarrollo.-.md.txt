# Plan de desarrollo Decidim Barcelona
_Informe técnico de la Direcció de Recerca, Desenvolupament i Innovació, Regidoría de Participació i Districtes_

_Ajuntament de Barcelona_

![Ajuntament de Barcelona](logo_ajbcn.jpg)

--------

## Resumen Ejecutivo

* Este documento detalla el futuro desarrollo de la **plataforma digital de participación de l´Ajuntament de Barcelona**, decidim.barcelona (disponible en URL [https://decidim.barcelona](https://decidim.barcelona)). 

### Marco

* En un contexto de creciente mediación tecnológica de la vida social y política, la **transición digital** de las estructuras gubernamentales se ha convertido en una oportunidad de **democratización**, pero también de **negocio**. Decidim.barcelona aspira a encarnar un modelo de **infraestructura democrática para la democracia**, una infraestructura digital de **código abierto, de producción y gestión público-común**. Este modelo **se opone al modelo privativo-corporativo** de plataforma digital, que hace de la extracción de datos, la provisión de servicios comerciales y la orientación de la conducta social un negocio masivo. Decidim.barcelona parte del software **Consul** (desarrollado por el Ayuntamiento de Madrid para su plataforma disponible en [https://decide.madrid.es](https://decide.madrid.es)), software libre, abierto y transparente.

### Plan de desarrollo 

* Los principales **objetivos de la plataforma** son articular, estandarizar, visualizar y comunicar todos los procesos de participación del Ajuntament de Barcelona y de la ciudad ofreciendo un servicio de infraestructura digital para la democracia directa y participativa a todas las escalas territoriales y asociativas de Barcelona. Estos objetivos llevarán consigo un incremento en la calidad de la plataforma, haciéndola cada vez más inclusiva, accesible, segura y respetuosa con la privacidad de las personas usuarias. También se busca facilitar el desarrollo de procesos y la auto-organización por parte de la ciudadanía, y ofrecer herramientas para la colaboración social. 

* Entre los aspectos clave del desarrollo de decidim.barcelona como proyecto sociotécnico se encuentran: la gobernanza, inicialmente llevada a cabo por la *Direcció de Recerca, Desenvolupament i Innovació* y que estará a cargo de la comunidad decidim a medio-largo plazo; el diseño tecnopolítico, que ha de atender tanto a las funcionalidades técnicas tanto como a los requisitos políticos y democráticos; la contratación y gestión del desarrollo del software, así como la administración de procesos participativos concretos; la investigación y evaluación de la actividad y dinámicas en la plataforma para mejorar la calidad democrática; la formación y capacitación crítica en el uso de la misma; por último, la coordinación del desarrollo de la plataforma con otros ayuntamientos e instituciones.

* El **flujo de desarrollo** está marcado por el tipo de programación **(desarrollo extremo)**, en el que el software se va adaptando a los cambios a la vez que se prueba en procesos de participación real, lo que implica satisfacer rápidamente funcionalidades o mejoras. El flujo se basa en lo propuesto inicialmente por el proyecto de software libre *git flow*[^1], diferenciando las siguientes ramas: **master**: es la versión estable, la que tomarán otras entidades que vayan a usar el software; **develop**: es la versión en desarrollo sobre la que se integran las demás ramas; **release**: acumula los desarrollos y las features para la siguiente versión estable, publicándose a través de releases de GitHub; **hotfixes**: sólo para corregir fallos rápidamente; **feature-X**: donde X son diferentes funcionalidades que pueden o constituir un hito o milestone concreto del master.

* La **arquitectura** es un aspecto clave del desarrollo del decidim a largo plazo. A fin de garantizar la **sostenibilidad, usabilidad y escalabilidad** se ha optado por un **desarrollo modular** sobre la aplicación web *Ruby on Rails*. El desarrollo estará basado en **Engines**, **componentes diferenciados para las distintas funcionalidades** (Propuestas, Debates, Legislación colaborativa, Citas presenciales, etc) y contará con mejoras en la documentación, tanto para su instalación como para su reutilización y adaptación por parte de otras entidades.  

* A fin de definir la **ontología** o conjunto de elementos del decidim se elabora un **glosario**, que define expresiones como  "proceso participativo", “espacios de participación, “componentes”, etc.

* En el documento se presentan las **funcionalidades descritas distribuidas en tres periodos: corto (2016), medio (2017) y largo plazo (2018)**. Asimismo se apuntan las **revisiones periódicas** a las que se someterá la plataforma, a fin de garantizar unos altos estándares de **apertura, privacidad, robustez y seguridad **en el código.

* Se calendarizan las **versiones** planeadas por el momento (0.5, en Octubre de 2016; 1, en Enero de 2017; y 1.5, en Marzo de 2017), así como los roles y gestión de usuarias en cada una. 

* También se define el **flujo de gestión de incidencias** mediante el uso de diferentes herramientas (como mailing y *Redmine*) y se definen los diferentes roles en el mismo. 

* El plan también detalla el carácter interdisciplinar, la organización y la estructura interna del **grupo de desarrollo**. El equipo está formado inicialmente por personas de  ámbitos diversos: **Ajuntament de Barcelona, universidades, profesionales especializados en programación**. A su vez el plan presenta el software usado para la coordinación y gestión de proyectos.

* Más tarde se presenta el **MetaDecidim**, un espacio en el decidim.barcelona y un proceso participativo para (re)diseñar las funcionalidades de la plataforma, priorizar las líneas de desarrollo, decidir proyectos de mejora y deliberar sobre los usos y posibilidades futuras de la herramienta. Metadecidim servirá también para crear una comunidad y un ecosistema de producción que ponga sobre la mesa el papel de gran calado democrático que representa la plataforma para la ciudadanía.

* **Más allá del decidim.barcelona**, se apuntan las posibilidades de una red de producción popular y gobernanza comunitaria  para las Superillas. 

* En el apéndice se define uno de los elementos innovadores del decidim.barcelona, la estructura del **configurador de procesos participativos**. 

* El plan se cierra proponiendo decidim.barcelona como infraestructura democrática para la democracia, base para la **democracia del futuro, hoy.**

##  Metadatos

<table>
  <tr>
    <td>Título</td>
    <td>Plan de desarrollo Decidim Barcelona</td>
  </tr>
  <tr>
    <td>Versión</td>
    <td>1.0</td>
  </tr>
  <tr>
    <td>Fecha</td>
    <td>14/11/2016</td>
  </tr>
  <tr>
    <td>Editores</td>
    <td>Andrés Pereira de Lucena, Xabier E. Barandiaran, Arnau Monterde, Juan Linares, Antonio Calleja-López</td>
  </tr>
  <tr>
    <td>Autores</td>
    <td>Xabier E. Barandiaran, Andrés Pereira de Lucena, Arnau Monterde, Antonio Calleja-López</td>
  </tr>
  <tr>
    <td>Resumen</td>
    <td>Este documento detalla el futuro desarrollo de la plataforma digital de participación de l´Ajuntament de Barcelona, decidim.barcelona (disponible en URL https://decidim.barcelona). Los principales objetivos de la plataforma son articular, estandarizar, visualizar y comunicar todos los procesos de participación del Ajuntament de Barcelona y de la ciudad ofreciendo un servicio de infraestructura digital para la democracia directa y participativa a todas las escalas territoriales y asociativas de Barcelona. El documento detalla los objetivos de la plataforma, el flujo de desarrollo, las funcionalidades previstas, y un código ético-político.</td>
  </tr>
  <tr>
    <td>Palabras Clave</td>
    <td>Plataforma digital de participación, red política, participación, decidim, consul, democracia digital</td>
  </tr>
  <tr>
    <td>Historia del documento</td>
    <td>Este documento se comenzó a construir de cara a ordenar y prever los recursos y las necesidades de desarrollo, de administración y de uso institucional de la plataforma digital de participación del Ajuntament de Barcelona en un contexto complejo y cambiante. Parte de los contenidos de este documento son heredados de varios espacios de colaboración del equipo de diseño tecnopolítico de Decidim Barcelona y del documento de planificación estratégica de la Direcció de I+D+i de la Regidoria de Participació i Districtes.</td>
  </tr>
  <tr>
    <td>Cómo citar</td>
    <td>Barandiaran, X.E., Pereira, A., Monterde, A. & Calleja-López A., Linares, J. (2016) Plan de desarrollo decidim.barcelona. Informe técnico de la Direcció de Recerca, Desenvolupament i Innovació, Regidoría de Participació i Districtes, Ajuntament de Barcelona.</td>
  </tr>
  <tr>
    <td>Copyleft</td>
    <td>Ajuntament de Barcelona y personas autoras del texto, bajo las licencias Creative Commons BY-SA (Reconocimiento Compartir Igual) Internacional (v.4.0) y GFDL (Licencia de Documentación Libre de GNU)
CC BY-SA: Creative Commons Reconocimiento Compartir Igual 4.0 Internacional
Usted es libre de copiar y redistribuir el material en cualquier medio o formato, remezclar, transformar y crear a partir del material, para cualquier finalidad, incluso comercial. El licenciador no puede revocar estas libertades mientras cumpla con los términos de la licencia. Bajo las siguientes condiciones: a) Reconocimiento: debe reconocer adecuadamente la autoría, proporcionar un enlace a la licencia e indicar si se han realizado cambios. Puede hacerlo de cualquier manera razonable, pero no de una manera que sugiera que tiene el apoyo del licenciador o lo recibe por el uso que hace; b) compartir igual: si remezcla, transforma o crea a partir del material, deberá difundir sus contribuciones bajo la misma licencia que el original. No hay restricciones adicionales, no puede aplicar términos legales o medidas tecnológicas que legalmente restrinjan realizar aquello que la licencia permite. Puede encontrar las licencias completas en los siguientes enlaces: https://creativecommons.org/licenses/by-sa/4.0/deed.es_ES 
GFDL: Licencia de Documentación Libre de GNU
Se concede permiso para copiar, distribuir y/o modificar este documento bajo los términos de la licencia de documentación libre GNU, versión 1.3 o cualquier otra versión posterior publicada por la Free Software Foundation; sin secciones invariantes ni textos de cubierta delantera, tampoco textos de contraportada. Una copia de la licencia se puede encontrar en http://www.gnu.org/copyleft/fdl.html
</td>
  </tr>
</table>

## Criterios de autoría y cómo participar en este documento [^2]

Este documento se abrirá a la participación. Podrás contribuir a este documento de varias formas diferentes. Excepto la función de edición el resto de las formas de participación y los niveles y criterios de autoría se especifican a continuación:

* *Editor/a:* Se encarga de la monitorización del texto, sus versiones, correcciones, estructuración, etc. Puede coincidir o no con alguna de las autoras. Se trata, en definitiva de un/a coordinador/a de la colaboración del texto. Es función del editor/a solicitar las revisiones y leerlas.

* *Autoras/es*: Son autoras/es quienes propiamente han redactado el texto. El orden de los autores refleja la contribución de los mismos siendo el primer nombre el de quien más ha escrito. El/la autor/a habrá leído y revisado el texto en su versión final o en versiones anteriores pero no tiene por qué estar de acuerdo con la configuración final del texto, labor que queda en manos del o la editora.

* *Contribuidor/a*: Aquí pueden considerarse dos grupos de contribuidores. Por una parte, los y las revisoras académicas del documento (en caso de que su contribución sea considerable) y, por otra, colaboradores/as externos/as cuya contribución haya sido de valor y se haya consolidado en partes de texto incluidas en el documento. La diferencia entre contribuidor y autor queda en manos del editor o del resto de autores pero, en todo caso, la contribución debe ser menor a la del resto de autoras/es. Como regla general, si un autor ha escrito menos del 10% del texto debería considerarse contribuidor/a. A su vez, ser contribuidor/a requiere al menos haber escrito dos o tres párrafos.

* *Participante*: Se trata de una persona que, sin haber contribuido con una parte de texto específica al documento, ha realizado contribuciones de valor, como comentarios pertinentes al mismo o ha proporcionado criterios, referencias o elementos de discusión valiosos.

* *Revisor/a*: Esta labor incluye una lectura minuciosa de todo el texto, la corrección de errores y la propuesta de mejoras al mismo. Por lo general, es un trabajo por encargo (solicitado a una persona que se considera competente en la materia), aunque es posible que alguien contribuya haciendo una revisión sin solicitud expresa. En tal caso, la profundidad y calidad de la misma pueden calificar para considerar a esta persona revisora.  

[^1]: Ver "A successful Git branching model" por Vincent Driessen publicado el 5 de enero de 2010 http://nvie.com/posts/a-successful-git-branching-model/

[^2]: Esta división y especificación de niveles de autoría se ha copiado directamente de los criterios establecidos en el proyecto FLOK Society - Buen conocer (véase: Barandiaran et al. 2015, pp.38-39).)
