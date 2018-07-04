# Guía de estilos para AngularJS

## Indice
  1. [AngularJS](#angularjs)
  1. [Responsabilidad Única](#single-responsibility-o-responsabilidad-única)
  1. [IIFE](#iife)
  1. [Módulos](#módulos)
  1. [Controladores](#controladores)
  1. [Servicios](#servicios)
  1. [Fábricas](#fábricas)
  1. [Servicios de Datos](#servicios-de-datos)
  1. [Directivas](#directivas)
  1. [Resolviendo Promesas en un Controlador](#resolviendo-promesas-en-un-controlador)
  1. [Anotación Manual para la Inyección de Dependencias](#anotación-manual-para-la-inyección-de-dependencias)
  1. [Minificación y Anotación](#minificación-y-anotación)
  1. [Manejo de Excepciones](#manejo-de-excepciones)
  1. [Estructura de la Aplicación El Principio LIFT](#estructura-de-la-aplicación-el-principio-lift)
  1. [Modularidad](#modularidad)
  1. [Lógica de Arranque](#lógica-de-arranque)
  1. [Servicios Envoltorios $ de Angular](#servicios-envoltorios--de-angular)
  1. [Pruebas](#pruebas)
  1. [Animaciones](#animaciones)
  1. [Comentarios](#comentarios)
  1. [Constantes](#constantes)
  1. [Plantillas y Snippets](#plantillas-y-snippets)
  1. [Ruteo](#ruteo)
  1. [Automatización de Tareas](#automatización-de-tareas)

## Inicio

### Para una guía de referencia sobre jade, stylus y js(es6) + plantilla para iniciar un proyecto con gulp: https://github.com/ifedu/styleguide-web

### Basada en la guías de estilos:
    - https://github.com/johnpapa/angular-styleguide/edit/master/i18n/es-ES.md

### Librerías usadas
    - AngularJs 1.3
        - Framework JS
        - Angular-ui-router
            - Simula redireccionamiento, útil para hace SPA

**[Indice](#indice)**

## `Single Responsibility` (Responsabilidad Única)

### La regla del 1

  - Define 1 componente por archivo.

  - El siguiente ejemplo define el módulo `app` y sus dependencias, define un controlador y define una fábrica todo en el mismo archivo.

```javascript
// MAL
angular
.module('app', ['ngRoute'])
.controller('SomeController', () => {})
.factory('someFactory', () => {})
```

  Los mismos componentes están separados en su propio archivo.

```javascript
// BIEN

// module.js
angular.module('app', ['ngRoute'])

// ctrl.js
angular.module('app')
.controller('SomeController', () => {})

// factory.js
angular.module('app')
.factory('someFactory', () => {})
```

**[Indice](#indice)**

## IIFE
### Closures de JavaScript

  - Envuelve los componentes AngularJS en una expresión de función(`function expression`) que se invoca inmediatamente Immediately Invoked Function Expression (IIFE).

  > ¿Por qué? Una IIFE elimina las variables del scope global. Esto ayuda a prevenir que las variables y las declaraciones de funciones vivan más de lo esperado en el scope global, evitando así colisión de variables.

  > ¿Por qué? Cuando tu código se minimiza y se empaqueta en un archivo único para desplegar al servidor de producción, podrías tener colisión de variables y muchas variables globales. Una IIFE te protege contra ambos, creando una scope por cada archivo.

```javascript
// MAL
// logger.js
angular
.module('app')
.factory('logger', logger);

// La función logger es añadida como variable global
function logger() { }

// storage.js
angular
.module('app')
.factory('storage', storage);

// La función storage es añadida como variable global
function storage() { }

// BIEN
// Así no dejamos ninguna variable global

// logger.js
(() => {
    angular.module('app')
    .factory('logger', logger)

    function logger() { }
})()

// storage.js
(() => {
    angular.module('app')
    .factory('storage', storage)

    function storage() { }
})()
```

  - Nota: Para acortar únicamente, el resto de los ejemplos de esta guía omiten la sintaxis IIFE.

  - Nota: IIFE previente que el código de los tests llegue a sus variables privadas, como expresiones regulares o funciones de ayuda que normalmente vienen bien para hacer pruebas por sí solas. Sin embargo, puedes acceder a ellas creando accesorios o accediendo a través de sus componentes. Por ejemplo, poniendo las funciones de ayuda, expresiones regulares o constantes en su propia fábrica.

**[Indice](#indice)**

## Módulos

### Evitando la colisión de nombres

  - Use una convención de nombres única con separadores para los sub-módulos.

  > ¿Por qué? Nombres únicos ayudan a evitar colisiones en los nombres de módulos. Los separadores ayudan a definir los módulos y la jerarquía de sus sub-módulos. Por ejemplo `app` puede ser tu módulo raíz y `app.dashboard` y `app.users` pueden ser módulos que dependen de `app`.

### Definiciones (`Setters`)

  - Declara los módulos sin usar una variable, usando la sintaxis de los setters.

  > ¿Por qué? Con un componente por archivo, es raro que necesitemos introducir una variable para el módulo.

```javascript
// MAL
const app = angular.module('app', [
    'app.dashboard',
    'app.shared',
    'ngAnimate',
    'ngRoute'
])
```

  En su lugar usa la sintaxis de los setters

```javascript
// BIEN
angular.module('app', [
    'app.dashboard',
    'app.shared',
    'ngAnimate',
    'ngRoute'
])
```

### Getters

  - Al usar un módulo, evita usar una variable y en su lugar usa encadenamiento con la sintaxis de los getter.

  > ¿Por qué? Esto hace más legible el código y evita que las variables colisionen.

```javascript
// MAL
var app = angular.module('app')
app.controller('SomeController', function() {
})

// BIEN
angular.module('app')
.controller('SomeController', function () {
})
```

### Setting vs Getting

  - Setea sólo una vez y usa get para el resto de instancias.

  > ¿Por qué? Un módulo debe ser creado sólo una vez y recuperado desde ese punto.

    - Usa `angular.module('app', []);` para setear un módulo.
    - Usa `angular.module('app');` para recuperar un módulo.

### Funciones anónimas vs funciones con nombre

  - No uses funciones con nombre usa funciones anónimas en el callback.

  > ¿Por qué? Así el código es más legible al tener la ejecución del código donde se va a ejecutar y reduce líneas de código que no aportan más que confusión.
  Las únicas excepciones para usar un nombre serían si la función esta en un fichero externo, o está varias veces repetida en el propio fichero.

  ```javascript
  // MAL
  angular
  .module('app')
  .controller('Dashboard', Dashboard)

  function Dashboard() { }
  ```

  ```javascript
  // BIEN
  angular
  .module('app')
  .controller('Dashboard', function() { })
  ```

**[Indice](#indice)**

## Controladores

### controllerAs Sintaxis en la Vista

  - Usa la sintaxis [`controllerAs`](http://www.johnpapa.net/do-you-like-your-angular-controllers-with-or-without-sugar/) en lugar del `clásico controlador con $scope`.

  > ¿Por qué? Los Controladores se construyen, renuevan y proporcionan una nueva instancia única, y la sintaxis `controllerAs` se acerca más a eso que la `sintaxis clásica de $scope`.

  > ¿Por qué? Promueves el uso de binding usando el "." en el objeto dentro de la Vista (ej. `customer.name` en lugar de `name`), así es más contextual, fácil de leer y evitas problemas de referencia que pueden aparecer con el "punto".

  > ¿Por qué? Ayuda a evitar usar `$parent` en las Vistas con controladores anidados.

```html
<!-- mal -->
div(ng-controller="CustomerCtrl") {{ name }}
```

```html
<!-- bien -->
div(ng-controller="Customer as customerCtrl") {{ customer.name }}
```

### controllerAs Sintaxis en el Controlador

  - La sintaxis `controllerAs` usa `this` dentro de los controladores que se asocian al `$scope`

  > ¿Por qué? `controllerAs` es azúcar sintáctico sobre el `$scope`. Puedes enlazar a la vista y acceder a los métodos del `$scope`.

  > ¿Por qué? Ayuda a evitar la tentación de usar los métodos del `$scope` dentro de un controller cuando debería ser mejor evitar usarlos o moverlos a una fábrica. Considera usar `$scope` en una factory, o en un controlador sólo cuando sea necesario. Por ejemplo cuando publicas y te suscribes a eventos usando [`$emit`](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$emit), [`$broadcast`](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$broadcast), o [`$on`](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$on) considera mover estos usos a una fábrica e invocarlos desde el controlador.

  ```javascript
  /* MAL */
  function Customer($scope) {
      $scope.name = {};
      $scope.sendMessage = function() { };
  }

  // BIEN
  function customer() {
      this.name = {}
      this.sendMessage = () => { }
  }
  ```

### controllerAs con vm

  - No usa una variable para capturar `this` cuando uses la sintaxis `controllerAs`, con los `function arrow` de `ES6` puedes llevar un control de `this`.

```javascript
// MAL
const customer = function () {
    this.name = 'Edu'
  
    const message = {
        // LA SINTAXIS CORTA ES IGUAL A PONER FUNCTION: send: function () {
        send() {
            // this HACE REFERENCIA A send Y NO ES LO QUE QUIERES
            console.log(this.name)
        }
    }

    message.send()
}

customer()

// BIEN
const customer = function () {
    this.name = 'Edu'
  
    const message = {
        send: () => {
            // this HACE REFERENCIA AL PARIENTE `function` MÁS CERCANO, EN ESTE CASO A customer
            console.log(this.name)
        }
    }

    message.send()
}

customer()
```

  Nota: Cuando crees watchers en un controlador usando `controller as`, puedes observar la variable `this.*` usando la siguiente sintaxis.(Crea los watchers con precaución ya que añaden mucha carga al ciclo de digest)

```html
input(ng-model="vm.title")
```

```javascript
function someCtrl($scope, $log) {
    this.title = 'Some Title'

    $scope.$watch('this.title', (current, original) => {
        $log.info('this.title was %s', original)
        $log.info('this.title is now %s', current)
    })
}
```

### Miembros Bindeables Arriba

  - No coloques asociaciones de variables por un lado y asignaciones por otra.

    > ¿Por qué? Esto sólo hace que sea más difícil de cambiar y dar seguimiento al código. Además añade líneas innecesarias dándole más complejidad.
    
  - Agrupa y siempre que sea viable alfabéticamente las variables primitivas, luego las compuestas y por último las funciones.
 
    *¿Por qué?: Esto hace que las variables sean fácilmente localizables y legibles.

```javascript
// MAL
function sessions() {
    this.gotoSession = gotoSession
    this.refresh = refresh
    this.search = search
    this.sessions = []
    this.title = 'Sessions'

    function gotoSession() {
        /* */
    }

    function refresh() {
        /* */
    }

    function search() {
        /* */
    }
}

// BIEN
function sessions() {
    this.title = 'Sessions'

    this.sessions = []

    this.gotoSession = () => {
        /* ... */
    }

    this.refresh = () => {
        /* ... */
    }

    this.search = () => {
        /* ... */
    }
}
```

### Declaraciones de Funciones para Esconder los Detalles de Implementación

  - Escribir expresiones de funciones(`function expression`) con `const` o `let` ayuda a no confiar en el `hoisting` de JavaScript y ver la ejecución secuencial de la web.
  - Escribir las funciones que se accedan sólo desde el html al final de las declaraciones.

```javascript
// MAL
function avengers(dataservice, logger) {
  var vm = this
  
  vm.avengers = []
  vm.getAvengers = getAvengers
  vm.title = 'Avengers'

  activate()

  function activate() {
      return getAvengers().then(function() {
          logger.info('Activated Avengers View')
      })
  }

  function getAvengers() {
      return dataservice.getAvengers().then(function(data) {
          vm.avengers = data
        
          return vm.avengers
      })
  }
}

// BIEN
const avengers = (dataservice, logger) => {
    this.title = 'Avengers'

    this.avengers = []

    const activate = () =>
        this
        .getAvengers()
        .then(() => logger.info('Activated Avengers View'))

    this.getAvengers = () =>
        dataservice
        .getAvengers()
        .then((data) => {
            this.avengers = data
          
            return this.avengers
        })

    activate()
}
```

### Diferir la Lógica del Controlador

  - Difiera la lógica dentro de un controlador delegándola a servicios y fábricas.

    > ¿Por qué? La lógica podría ser reutilizada por varios controladores cuando la colocas en un servicio y la expones como una función.

    > ¿Por qué? La lógica en un servicio puede ser aislada en un test unitario, mientras que la lógica de llamadas en un controlador se puede mockear fácilmente.

    > ¿Por qué? Elimina dependencias y esconde detalles de implementación del controlador.

  ```javascript

// MAL
function order($http) {
    this.total = 0

    this.checkCredit = () =>
        $http
        .get([])
        .then((data) => this.isCreditOk = (this.total <= maxRemainingAmount))
        .catch((error) => // Interpret error)
}

// BIEN
function Order(creditService) {
    this.total = 0

    this.checkCredit() =>
        creditService
        .isOrderTotalOk(this.total)
        .then((isOk) => this.isCreditOk = isOk)
        .catch(creditService.showError)
}
```

### Mantén tus Controladores Enfocados

  - Define un controlador para una vista, no intentes reutilizar el controlador para otras vistas. En lugar de eso, mueve la lógica que se pueda reutilizar a fábricas y deja el controlador simple y enfocado en su vista.

    > ¿Por qué? Reutilizar controladores con varias vistas es arriesgado y necesitarías buena cobertura de tests `end to end` (e2e) para asegurar que todo funciona bien en la aplicación.

### Asignando Controladores

  - Cuando un controlador debe ser asociado a una vista y cada componente puede ser reutilizado por otros controladores o vistas, define controladores con sus rutas.

    Nota: Si una Vista es cargada por otra además de por la ruta, entonces usa la sintaxis `ng-controller="AvengersCtrl as avengersCtrl"`.

    > ¿Por qué? Emparejar el controlador en la ruta permite a diferentes rutas invocar diferentes pares de controladores y vistas. Cuando los controladores son asignados en la vista usando [`ng-controller`](https://docs.angularjs.org/api/ng/directive/ngController), esa vista siempre estará asociada al mismo controlador.

 ```javascript
// MAL - cuando se use con una ruta y queramos asociarlo dinámicamente
// route-config.js
angular
.module('app')
.config(function($routeProvider) {
    $routeProvider
    .when('/avengers', {
        templateUrl: 'avengers.html'
    })
})
```

```html
<!-- avengers.html -->
div(ng-controller="AvengersCtrl as avengersCtrl")
```

```javascript
// BIEN
// route-config.js
angular
.module('app')
.config(function ($routeProvider) {
    $routeProvider.when('/avengers', {
        templateUrl: 'avengers.html',
        controller: 'AvengersCtrl',
        controllerAs: 'avengersCtrl'
    })
})
```

```html
<!-- avengers.html -->
div
```

**[Indice](#indice)**

## Servicios

### Singletons

  - Los Servicios son instanciados con un `new`, usan `this` para los métodos públicos y las variables. Ya que son muy similares a las factories, usa una factory en su lugar por consistencia.

    Nota: [Todos los servicios AngularJS son singletons](https://docs.angularjs.org/guide/services). Esto significa que sólo hay una instancia de un servicio por inyector.

```javascript
// service
angular
.module('app')
.service('logger', function () {
    this.logError = (msg) => {
        /* */
    }
})

// factory
angular
.module('app')
.factory('logger', function () {
    return {
        logError: (msg) => {
            /* */
        }
    }
})
```

**[Indice](#indice)**

## Fábricas

### Responsabilidad Única

  - Las fábricas deben tener una [responsabilidad única](http://en.wikipedia.org/wiki/Single_responsibility_principle), que es encapsulada por su contexto. Cuando una fábrica empiece a exceder el principio de responsabilidad única, una nueva fábrica debe ser creada.

### Singletons

  - Las Fábricas son singleton y devuelven un objeto que contiene las variables del servicio.

    Nota: [Todos los servicios AngularJS son singletons](https://docs.angularjs.org/guide/services).

### Miembros accesibles Arriba

  - Devuelve directamente el objeto a usar, ordena las propiedades y luego los métodos alfabéticamente, deja un espacio entre las propiedades primitivas y los métodos, así como entre métodos y propiedades complejas.

    > ¿Por qué? Reducirás el número de líneas y aumentarás la legibilidad.

```javascript
// MAL
function dataService() {
    let someValue = ''

    const save = () => {
        /* */
    }

    const validate = () => {
        /* */
    }

    return {
        save: save,
        someValue: someValue,
        validate: validate
    }
}

// MAL
function dataService() {
    let someValue = ''

    const service = {
        save,
        someValue,
        validate
    }
  
    return service

    function save() {
        /* */
    }

    function validate() {
        /* */
    }
}

// BIEN
function dataService() {
    return {
        someValue: '',

        save() {
            // CÓDIGO
        },

        validate() {
            // CÓDIGO
        }
    }
}

// MAL
function dataservice($http, $location, $q, exception, logger) {
    let isPrimed = false
    let primePromise

    const getAvengers = function() {
        // CÓDIGO
    }

    const getAvengerCount = function() {
        // CÓDIGO
    }

    const getAvengersCast = function() {
        // CÓDIGO
    }

    const prime = function() {
        // CÓDIGO
    }

    const ready = function(nextPromises) {
        // CÓDIGO
    }

    const service = {
        getAvengersCast: getAvengersCast,
        getAvengerCount: getAvengerCount,
        getAvengers: getAvengers,
        ready: ready
    }

    return service
}

// MAL
function dataservice($http, $location, $q, exception, logger) {
    let isPrimed = false
    let primePromise

    const service = {
        getAvengersCast,
        getAvengerCount,
        getAvengers,
        ready
    }

    return service

    ////////////

    function getAvengers() {
        // CÓDIGO
    }

    function getAvengerCount() {
        // CÓDIGO
    }

    function getAvengersCast() {
        // CÓDIGO
    }

    function prime() {
        // CÓDIGO
    }

    function ready(nextPromises) {
        // CÓDIGO
    }
}

// BIEN
function dataservice($http, $location, $q, exception, logger) {
    let isPrimed = false
    let primePromise

    return {
        getAvengersCast() {
            // CÓDIGO
        },

        getAvengerCount() {
            // CÓDIGO
        },

        getAvengers() {
            // CÓDIGO
        },

        ready() {
            // CÓDIGO
        }
    }
}
```

**[Indice](#indice)**

## Servicios de Datos

### Separate Data Calls

  - Refactoriza la lógica para hacer operaciones e interaciones con datos en una factory. Crear data services responsables de las peticiones XHR, local storage, memoria o cualquier otra operación con datos.

    > ¿Por qué? La responsabilidad del controlador es la de presentar y recoger información para la vista. No debe importarle cómo se consiguen los datos, sólo saber cómo conseguirlos. Separando los datos de servicios movemos la lógica de cómo conseguirlos al servicio de datos, y deja el controlador simple, enfocándose en la vista.

    > ¿Por qué? Hace más fácil testear (mock o real) las llamadas de datos cuando testeamos un controlador que usa un data service.

    > ¿Por qué? La implementación del servicio de datos puede tener código muy específico para usar el repositorio de datos. Podría incluir cabeceras, cómo hablar a los datos, u otros servicios como $http. Separando la lógica en servicios de datos encapsulamos la lógica en un único lugar, escondiendo la implementación de sus consumidores externos (quizá un controlador), de esta forma es más fácil cambiar la implementación.

```javascript
// MAL
// dataservice factory
angular
.module('app.core')
.factory('dataservice', dataservice)

dataservice.$inject = ['$http', 'logger']

function dataservice($http, logger) {
    return {
        getAvengers: getAvengers
    }

    function getAvengers() {
        return $http
            .get('/api/maa')
            .then(getAvengersComplete)
            .catch(getAvengersFailed);

        function getAvengersComplete(response) {
            return response.data.results;
        }

        function getAvengersFailed(error) {
            logger.error('XHR Failed for getAvengers.' + error.data);
        }
    }
}

// BIEN
// dataservice factory
angular.module('app.core')
.factory('dataservice', ($http, logger) => {
    return {
        getAvengers() {
            return $http
                .get('/api/maa')
                .then(() => response.data.results)
                .catch(() => logger.error('XHR Failed for getAvengers.' + error.data))
        }
    }
})
```

    Nota: El servicio de datos es llamado desde los consumidores, como el controlador, escondiendo la implementación del consumidor como se muestra a continuación.

```javascript
// MAL
// controller llamando a la factory del data service
angular
.module('app.avengers')
.controller('Avengers', Avengers);

Avengers.$inject = ['dataservice', 'logger'];

function Avengers(dataservice, logger) {
    var vm = this
    vm.avengers = []

    activate()

    function activate() {
        return getAvengers().then(function() {
            logger.info('Activated Avengers View')
        })
    }

    function getAvengers() {
        return dataservice
            .getAvengers()
            .then(function(data) {
                vm.avengers = data
                return vm.avengers
            })
    }
}
// BIEN
// controller llamando a la factory del data service
angular
.module('app.avengers')
.controller('Avengers', function (dataservice, logger) {
    this.avengers = []

    const activate = () =>
        getAvengers()
        .then(() => logger.info('Activated Avengers View'))
    }

    const getAvengers = () =>
        dataservice
        .getAvengers()
        .then((data) => {
            this.avengers = data

            return this.avengers
        })
    }

    activate()
}
```

### Regresa una Promesa desde las Llamadas a Datos

  - Cuando llamamos a servicios de datos que devuelven una promesa como $http, devuelve una promesa en la llamada de tu función también.

    > ¿Por qué? Puedes encadenar promesas y hacer algo cuando la llamada se complete y resuelva o rechace la promesa.

```javascript
// BIEN
const getAvengers = () =>
    /*
       Step 2
       Pide al servicio de datos los datos y espera por la promesa
    */
    dataservice
    .getAvengers()
    .then((data) => {
        /*
           Step 3
           setea los datos y resuelve la promesa
        */
        this.avengers = data;
        
        return this.avengers
    })

const activate = () =>
    getAvengers().then(() => {
        /*
           Step 4
           Ejecuta una acción cuando se resuelva la promesa final
        */
        logger.info('Activated Avengers View')
    })

activate()
```

    **[Indice](#indice)**

## Directivas
### Limitadas a 1 Por Archivo

  - Crea una directiva por archivo. Llama al archivo como la directiva.

    > ¿Por qué? Es muy fácil colocar todas las directivas en un archivo, pero será más difícil de partir para ser compartida entre aplicaciones, módulos o para un simple módulo.

    > ¿Por qué? Una directiva por archivo es fácil de mantener.

```javascript
// MAL
/* directives.js */

angular
.module('app.widgets')

// directiva de órdenes que es específica del módulo de órdenes
.directive('orderCalendarRange', orderCalendarRange)

// directiva de ventas que puede ser usada en algún otro lado a lo largo de la aplicación de ventas
.directive('salesCustomerInfo', salesCustomerInfo)

// directiva de spinner que puede ser usada a lo largo de las aplicaciones
.directive('sharedSpinner', sharedSpinner);

function orderCalendarRange() {
    // CÓDIGO
}

function salesCustomerInfo() {
    // CÓDIGO
}

function sharedSpinner() {
    // CÓDIGO
}

// BIEN
// calendarRange.directive.js
angular
.module('sales.order')
.directive('acmeOrderCalendarRange', function () {
    // CÓDIGO
})

// customerInfo.directive.js
angular
.module('sales.widgets')
.directive('acmeSalesCustomerInfo', function () {
    // CÓDIGO
})

// spinner.directive.js
angular
.module('shared.widgets')
.directive('acmeSharedSpinner', function () {
    // CÓDIGO
})
```

    Nota: Hay muchas formas de llamar a las directivas, especialmente cuando pueden ser usadas en ámbitos específicos. Elige un nombre que tenga sentido para la directiva y que su archivo sea distintivo y claro. Hemos visto algunos ejemplos antes, pero veremos más en la sección de cómo nombrar.

### Manipula el DOM en una Directiva

  - Cuando manipules DOM directamente, usa una directiva. Si hay alguna alternativa como usando CSS para cambiar los estilos o los [animation services](https://docs.angularjs.org/api/ngAnimate), Angular templating, [`ngShow`](https://docs.angularjs.org/api/ng/directive/ngShow) o [`ngHide`](https://docs.angularjs.org/api/ng/directive/ngHide), entonces úsalos en su lugar. Por ejemplo, si la directiva sólo muestra o esconde elementos, usa ngHide/ngShow.

    > ¿Por qué? Manipular el DOM puede ser difícil de testear, debugear y normalmente hay mejores maneras (e.g. CSS, animations, templates)

### Provee un Prefijo Único de Directiva

  - Proporciona un prefijo corto, único y descriptivo como `acmeSalesCustomerInfo` que se declare en el HTML como `acme-sales-customer-info`.

    > ¿Por qué? El prefijo corto y único identifica el contexto de la directiva y el origen. Por ejemplo el prefijo `cc-` puede indicar que la directiva en particular es parte de la aplicación CodeCamper, mientras que `acme-` pudiera indicar que la directiva es de la compañía Acme.

    Nota: Evita `ng-` ya que está reservado para las directivas AngularJS. Estudia sabiamente las directivas usadas para evitar conflictos de nombres, como `ion-` de [Ionic Framework](http://ionicframework.com/).

### Limitate a Elementos y Atributos

  - Cuando crees directivas que tengan sentido como elemento, restringe `E` (elemento personalizado) y opcionalmente restringe `A` (atributo personalizado). Generalmente, si puede ser su control propio, `E` es apropiado, La pauta general es permitir `EA` pero intenta implementarlo como un elemento cuando sea un elemento único y como un atributo cuando añada mejoras a su propio elemento existente en el DOM.

    > ¿Por qué? Mientras permitamos que una directiva sea usada como una clase, si esa directiva realmente está actuando como un elemento, tiene sentido que sea un elemento, o al menos un atributo.

    Nota: En AngularJS 1.3+ EA es el valor por defecto

```html
// MAL
.my-calendar-range
```

```javascript
angular
.module('app.widgets')
.directive('myCalendarRange', function () {
    var directive = {
        link: link,
        templateUrl: '/template/is/located/here.html',
        restrict: 'C'
    }
  
    return directive

    function link(scope, element, attrs) {
        // CÓDIGO
    }
})
```

```html
// BIEN
my-calendar-range
div(my-calendar-range)
```

```javascript
angular
.module('app.widgets')
.directive('myCalendarRange', () => {
    return {
        restrict: 'EA',
        templateUrl: '/template/is/located/here.html',
      
        link() {
            // CÓDIGO
        }
    }
}
```

### Directivas y ControllerAs

  - Usa la sintaxis `controller as` con una directiva para ser consistente con el uso de `controller as` con los pares de vista y controlador.

    Nota: La siguiente directiva demuestra algunas de las formas en las que puedes usar el scope dentro del link y el controlador de una directiva, usando controllerAs. He puesto la template para dejarlo todo en un lugar.

    Nota: En cuanto a la inyección de dependencias, mira [Identificar Dependencias Manualmente](#manual-annotating-for-dependency-injection).

    Nota: Nótese que el controlador de la directiva está fuera del closure de la directiva. Este estilo elimina los problemas que genera la inyección de dependencias donde la inyección es creada en un código no alcanzable después del `return`.

```html
div(
    max="77"
    my-example
)
```

```javascript
angular
.module('app')
.directive('myExample', function ($scope) {
    return {
        bindToController: true, // porque el scope is aislado
        controllerAs: 'myExampleCtrl',
        restrict: 'EA',
        templateUrl: 'app/feature/example.directive.html',

        scope: {
            max: '='
        },

        controller($scope) {
            // Inyectando el $scope solo para comparación
            this.min = 3
    
            console.log('CTRL: $scope.myExampleCtrl.min = %s', $scope.myExampleCtrl.min)
            console.log('CTRL: $scope.myExampleCtrl.max = %s', $scope.myExampleCtrl.max)
            console.log('CTRL: mymyExampleCtrl.min = %s', this.min)
            console.log('CTRL: mymyExampleCtrl.max = %s', this.max)
        },

        link(scope, el, attr, ctrl) {
            console.log('LINK: scope.min = %s *** should be undefined', scope.min)
            console.log('LINK: scope.max = %s *** should be undefined', scope.max)
            console.log('LINK: scope.myExampleCtrl.min = %s', scope.myExampleCtrl.min)
            console.log('LINK: scope.myExampleCtrl.max = %s', scope.myExampleCtrl.max)
        }
    }
}
```

```html
//example.directive.html
div hello world
div (max={{myExampleCtrl.max}})
    input(ng-model="myExampleCtrl.max")
div(min={{myExampleCtrl.min}})
    input(ng-model="myExampleCtrl.min")
```

  - Usa `bindToController = true` cuando uses `controller as` con una directiva cuando quieras asociar el scope exterior al scope del controller de la directiva.

    > ¿Por qué? Lo hace más fácil a la hora de asociar el scope exterior al scope del controlador de la directiva.

    Nota: `bindToController` fue introducido en Angular 1.3.0.

```html
div(
  max="77"
  my-example
)
```

```javascript
angular
.module('app')
.directive('myExample', function () {
    return {
        bindToController: true,
        controllerAs: 'exampleCtrl',
        restrict: 'EA',
        templateUrl: 'app/feature/example.directive.html',

        scope: {
            max: '='
        },

        controller() {
            this.min = 3

            console.log('CTRL: this.min = %s', this.min)
            console.log('CTRL: this.max = %s', this.max)
        }
    }
}
```

```html
<!-- example.directive.html -->
<div>hello world</div>
<div>max={{exampleCtrl.max}}<input ng-model="exampleCtrl.max"/></div>
<div>min={{exampleCtrl.min}}<input ng-model="exampleCtrl.min"/></div>
```

**[Indice](#indice)**

## Resolviendo Promesas en un Controlador

### Promesas de Activación de un Controlador

  - No uses funciones si no son necesarias.

    > ¿Por qué? Añades líneas y complejidad a la página innecesarias, usa siempre variables descriptivas y si fuese necesario como apoyo algún comentario.

```javascript
// MAL
function avengersCtrl(dataservice) {
    var vm = this

    vm.avengers = []
    vm.title = 'Avengers'

    activate()

    function activate() {
        dataservice
        .getAvengers()
        .then((data) => {
            vm.avengers = data

            return vm.avengers
        })
    }
}

// BIEN
function avengersCtrl(dataservice) {
    this.avengers = []
    this.title = 'Avengers'

    //ACTIVATE
    dataservice
    .getAvengers()
    .then((data) => {
        this.avengers = data

        return this.avengers
    })
}
```

### Resolución de Promesas en la Ruta

  - Cuando un controlador depende en una promesa a ser resuelta antes de que el controlador se active, resuelve esas dependencias en el `$routeProvider` antes de que la lógica del controlador sea ejecutada. Si necesitas condicionalmente cancelar una ruta antes de que el controlador sea activado, usa un route resolver.

  - Usa un route resolver cuando decidas cancelar la ruta antes de hacer la transición a la Vista.

    > ¿Por qué? Un controlador puede requerir datos antes de que se cargue. Esos datos deben venir desde una promesa a través de una fábrica o de [$http](https://docs.angularjs.org/api/ng/service/$http). Usando un [route resolve](https://docs.angularjs.org/api/ngRoute/provider/$routeProvider) permite que la promesa se resuelva antes de que la lógica del controlador se ejecute, así puedes tomar decisiones basándote en los datos de la promesa.

    > ¿Por qué? El código se ejecuta después de la ruta y la función activate del controlador. La Vista empieza a cargar al instante. El bindeo de los datos se ejecutan cuando la promesa del activate se resuelva. Una animación de "Cargando" se puede mostrar durante la transición de la vista (via ng-view o ui-view)

    Nota: El código se ejecuta antes que la ruta mediante una promesa. Rechazar la promesa cancela la ruta. Resolverla hace que la nueva vista espere a que la ruta sea resuelta. Una animación de "Cargando" puede ser mostrada antes de que se resuelva. Si quieres que la Vista aparezca más rápido y no necesitas un checkpoint para decidir si puedes mostrar o no la view.

```javascript
// MAL
angular
.module('app')
.controller('avengers', function (movieService) {
    // sin resolver
    this.movies

    // resulta asincronamente
    movieService.getMovies()
    .then((response) => this.movies = response.movies)
})

// BIEN
// route-config.js
angular
.module('app')
.config(($routeProvider) => {
    $routeProvider.when('/avengers', {
        controller: 'AvengersCtrl',
        controllerAs: 'avengersCtrl',
        templateUrl: 'avengers.html',

        resolve: {
            moviesPrepService(movieService) {
                return movieService.getMovies()
            }
        }
    })
}

// avengers.js
angular
.module('app')
.controller('AvengersCtrl', function (moviesPrepService) {
    this.movies = moviesPrepService.movies
})
```
**[Indice](#indice)**

## Manejo de Excepciones

### Decoradores

  - Usa un decorador o [decorator](https://docs.angularjs.org/api/auto/service/$provide#decorator), en tiempo de configuración usando el servicio [`$provide`](https://docs.angularjs.org/api/auto/service/$provide), en el servicio [`$exceptionHandler`](https://docs.angularjs.org/api/ng/service/$exceptionHandler) para realizar acciones personalizadas cuando una excepción ocurra.

    > ¿Por qué? Provee una manera consistente de manejar excepciones de AngularJS que no están siendo capturadas en tiempo de desarrollo o en tiempo de ejecución.

    Nota: Otra opción es sobreescribir el servicio en lugar de usar un decorador. Esto está bien, pero si quiere mantener el comportamiento por default y extenderlo se recomienda usar un decorador.

```javascript
// BIEN
angular
.module('blocks.exception')
.config(($provide) =>
    $provide.decorator('$exceptionHandler', ($delegate, toastr) =>
        function(exception, cause) {
            $delegate(exception, cause)

            const errorData = {
                cause,
                exception
            }
            /*
                Pudieramos agregar el error a la colección de un servicio,
                agregar los errores en el $rootScope,
                logear los errores a un servidor remoto,
                o logear localmente. O arrojarlos llanamente.
                Dependende totalmente de tí.
                arrojar excepción;
            */
            toastr.error(exception.msg, errorData)
        }
    )
)
```

### Cachadores de Excepciones

  - Crea una fábrica que exponga una interfaz para cachar y manejar excepciones elegantemente.

    > ¿Por qué? Provee de una manera consistente de cachar excepciones que puedan ser arrojadas en tu código (e.g. durante llamadas XHR o promesas que fallaron).

    Nota: El cachador de excepciones es bueno para cachar y reaccionar a excepciones específicas de llamadas que tu sabes van a arrojar una. Por ejemplo, al hacer una llamada XHR para obtener datos desde un servicio web remoto y quieres cachar cualquier excepción de ese servicio y reaccionar únicamente.

```javascript
// BIEN
angular
.module('blocks.exception')
.factory('exception', (logger) => {
    return {
        catcher(message) {
            return function (reason) {
                logger.error(message, reason)
            }
        }
    }
}
```

### Errores de Ruta

  - Maneja y logea todos los errores de enrutamiento usando [`$routeChangeError`](https://docs.angularjs.org/api/ngRoute/service/$route#$routeChangeError).

    > ¿Por qué? Provee una manera consistente de manejar todos los errores de enrutamiento.

    > ¿Por qué? Potencialmente provee una mejor experiencia de usuario si un error de enrutamiento ocurre y tu los rediriges a una pantalla amigable con más detalles u opciones de recuperación.

```javascript
// BIEN
function handleRoutingErrors() {
    /*
        Route cancellation:
        Cancelación de la Ruta:
        En un error de ruteo, ir al dashboard.
        Proveer una cláusula de salida si trata de hacerlo dos veces.
    */
    $rootScope.$on('$routeChangeError', (event, current, previous, rejection) => {
        const DESTINATION = (current && (current.title || current.name || current.loadedTemplateUrl)) || 'unknown target'
       
        const MSG = `Error routing to ${DESTINATION}. ` + (rejection.msg || '')
        /*
            Optionally log using a custom service or $log.
            Opcionalmente logear usando un servicio personalizado o $log.
            (Don't forget to inject custom service)
        */
        logger.warning(MSG, [current])
    })
}
```

**[Indice](#indice)**

## Estructura de la Aplicación El Principio LIFT
### LIFT

  - Estructura tu aplicación de tal manera que puedas Localizar (`L`ocate) tu código rápidamente, Identificar (`I`dentify) el código de un vistazo, mantener la estructura más plana (`F`lattest) que puedas, y Trata (`T`ry) de mantenerte DRY. La estructura debe de seguir estas 4 pautas básicas.

    *¿Por qué LIFT?*: Provee una estructura consistente que escala bien, es modular, y hace más fácil incrementar la eficiencia de los desarrolladores al encontrar código rápidamente. Otra manera de checar la estructura de tu aplicación es preguntarte a ti mismo: ¿Qué tan rápido puede abrir y trabajar en todos los archivos relacionados a una caracteristica?

    Cuando encuentro que mi estructura no se siente cómoda, regreso y reviso estas pautas LIFT

    1. `L`ocating - Localizar nuestro código es fácil
    2. `I`dentify - Identificar código de un vistazo
    3. `F`lat - Estructura plana tanto como sea posible
    4. `T`ry - Tratar de mantenerse DRY (Don't Repeat Yourself) or T-DRY

**[Indice](#indice)**

## Lógica de Arranque
### Configuración

  - Inyecta código dentro de [module configuration](https://docs.angularjs.org/guide/module#module-loading-dependencies) que necesite ser configurado antes de correr la aplicación angular. Candidatos ideales incluyen providers y constantes.

    > ¿Por qué? Esto hace más fácil tener menos lugares para la configuración.

```javascript
angular
.module('app')
.config((routerHelperProvider, exceptionHandlerProvider, toastr) => {
    exceptionHandlerProvider.configure(config.appErrorPrefix)

    routerHelperProvider.configure({
        docTitle: 'NG-Modular: '
    })

    toastr.options.positionClass = 'toast-bottom-right'
    toastr.options.timeOut = 4000
})
```

### Bloques Run

  - Cualquier código que necesite ser ejecutado cuando una aplicación arranca debe ser declarado en una fábrica, ser expuesto a través de una función, o inyectado en el [bloque run](https://docs.angularjs.org/guide/module#module-loading-dependencies).

    > ¿Por qué? Código que está directamente en un bloque run puede ser difícil de testear. Colocarlo en una fábrica lo hace fácil de abstraer y mockear.

```javascript
angular
.module('app')
.run((authenticator, translator) => {
    authenticator.initialize()
    translator.initialize()
})
```

**[Indice](#indice)**

## Servicios Envoltorios $ de Angular

### $document y $window

  - Usa [`$document`](https://docs.angularjs.org/api/ng/service/$document) y [`$window`](https://docs.angularjs.org/api/ng/service/$window) en lugar de `document` y `window`.

    > ¿Por qué? Estos servicios son envueltos por Angular y son más fáciles de testear en lugar de usar document y window en las pruebas. Esto te ayuda a evitar que tener que mockear document y window tu mismo.

### $timeout y $interval

  - Usa [`$timeout`](https://docs.angularjs.org/api/ng/service/$timeout) y [`$interval`](https://docs.angularjs.org/api/ng/service/$interval) en lugar de `setTimeout` y `setInterval` .

    > ¿Por qué? Estos servicios están envueltos por Angular y son más fáciles de testear y manejar el ciclo digest de AngularJS así que mantienen el bindeo de los datos en sincronización.

**[Indice](#indice)**

## Pruebas
Las pruebas unitarias ayudan a mantener el código limpio, así que incluyo algunas de mis recomendaciones en los fundamentos del testeo unitario con links para mayor información.

### Escribe Pruebas con Historias

  - Escribe un conjunto de pruebas para cada historia. Comienza con un test vacío y llénalo conforme escribas el código para la historia.

    > ¿Por qué? Escribir descripciones para la prueba ayuda a definir claramente qué es lo que tu historia hará, qué no hará, y cómo puedes medir el éxito.

    ```javascript
    it('should have Avengers controller', () => {
        // TODO
    })

    it('should find 1 Avenger when filtered by name', () => {
        // TODO
    })

    it('should have 10 Avengers', () => {
        // TODO (mock data?)
    })

    it('should return Avengers via XHR', () => {
        // TODO ($httpBackend?)
    })

    // y así
    ```

### Librería para las Pruebas

  - Usa [Jasmine](http://jasmine.github.io/) o [Mocha](http://mochajs.org) para las pruebas unitarias.

    > ¿Por qué? Ambas Jasmine y Mocha son usadas ampliamente por la comunidad de AngularJS. Ambas son estables, bien mantenidas, y proveen de características de pruebas robustas.

    Nota: Cuando uses Mocha, también considera elegir una librería como [Chai](http://chaijs.com).

### Test Runner

  - Usa [Karma](http://karma-runner.github.io) como test runner.

    > ¿Por qué? Karma es fácil de configurar para correr una vez o automáticamente cuando cambias tu código.

    > ¿Por qué? Karma encaja en tu proceso de Integración Continua fácilmente por sí sola o a través de Grunt o Gulp.

    > ¿Por qué? Algunos IDE's están comenzando a integrarse con Karma, tal como [WebStorm](http://www.jetbrains.com/webstorm/) y [Visual Studio](http://visualstudiogallery.msdn.microsoft.com/02f47876-0e7a-4f6c-93f8-1af5d5189225).

    > ¿Por qué? Karma funciona bien con líderes de automatización de tareas tales como [Grunt](http://www.gruntjs.com) (con [grunt-karma](https://github.com/karma-runner/grunt-karma)) y [Gulp](http://www.gulpjs.com) (con [gulp-karma](https://github.com/lazd/gulp-karma)).

### Stubear y Espíar
  - Usa [Sinon](http://sinonjs.org/) para el stubeo y espíar.

    > ¿Por qué? Sinon funciona bien con ambos Jasmine y Mocha y extiende las características de stubeo y espío que ellos ofrecen.

    > ¿Por qué? Sinon hace más fácil cambiar entre Jasmine y Mocha, si quieres probar ambos.

### Headless Browser
  - Usa [PhantomJS](http://phantomjs.org/) para correr tus pruebas en un servidor.

    > ¿Por qué? PhantomJS es un navegador headless que ayuda a correr las pruebas sin necesitar una navegador "visual". Así que no necesitas instalar Chrome, Safari u otros navegadores en tu servidor.

    Nota: Aún debes testear en todos los navegadores de tu entorno, así como sea apropiado para tu audiencia meta.

  ![Testing Tools](https://raw.githubusercontent.com/johnpapa/angularjs-styleguide/master/assets/testing-tools.png)

### Organizando las Pruebas

  - Coloca archivos de pruebas unitarias (specs) lado a lado con tu código del cliente. Coloca tus specs que cubren la integración con el servidor o que prueban múltiples componentes en un directorio `tests` separado.

    > ¿Por qué? Las Pruebas Unitarias tiene una correlación directa con un componente y archivo específico en tu código fuente.

    > ¿Por qué? Es más fácil mantenerlas actualizadas ya que siempre están a la vista. Al escribir código ya sea que realices TDD o pruebes durante el desarrollo o después del desarrollo, los specs están lado a lado y nunca fuera de la vista o de la mente, así es más probable que sean mantenidas lo cual ayuda a mantener la cobertura de pruebas.

    > ¿Por qué? Cuando actualices código fuente es más fácil ir y actualizar las pruebas al mismo tiempo.

    > ¿Por qué? Colocarlas lado a lado hace más fácil encontrarlas y fácil de moverlas con el código fuente si mueves la fuente.

    > ¿Por qué? Tener el spec cerca hace más fácil al lector del código fuente aprender cómo se supone que el componente es usado y descubrir sus propias limitaciones.

    > ¿Por qué? Separar specs para que no estén un build de distribución es fácil con grunt o gulp.

**[Indice](#indice)**

## Animaciones

### Uso

  - Usa sutiles [animaciones con AngularJS](https://docs.angularjs.org/guide/animations) para hacer transiciones entre estados en vistas y elementos visuales primarios. Incluye el [módulo ngAnimate](https://docs.angularjs.org/api/ngAnimate). Las 3 claves son sutil, fluido, transparente.

    > ¿Por qué? Animaciones sutiles pueden mejorar la Experiencia de Usuario cuando son usadas apropiadamente.

    > ¿Por qué? Animaciones sutiles pueden mejorar el rendimiento percibido como una transición de vista.

### Sub Segundos

  - Usa duraciones cortas para las animaciones. Generalmente empiezo con 300ms y ajusto hasta que es apropiado.

    > ¿Por qué? Animaciones largas pueden tener el efecto contrario en la Experiencia de Usuario y el rendimiento percibido al dar la apariencia de una aplicación lenta.

### animate.css

  - Usa [animate.css](http://daneden.github.io/animate.css/) para animaciones convencionales.

    > ¿Por qué? Las animaciones que animate.css provee son rápidas, fluidas, y fáciles de agregar en tu aplicación.

    > ¿Por qué? Provee consistencia en tus animaciones.

    > ¿Por qué? animate.css está ampliamente usado y testeado.

    Nota: Ve este [ excelente post de Matias Niemelä sobre animaciones AngularJS](http://www.yearofmoo.com/2013/08/remastered-animation-in-angularjs-1-2.html)

**[Indice](#indice)**

## Enrutamiento
Enrutamiento del lado del Cliente es importante para crear un flujo de navegación entre vistas y vistas de composición que están hechas de muchas pequeñas plantillas y directivas.

  - Usa el [AngularUI Router](http://angular-ui.github.io/ui-router/) para ruteo del lado del cliente.

    > ¿Por qué? UI Router ofrece todas las características del router de Angular mas algunas adicionales incluyendo rutas anidadas y estados.

    > ¿Por qué? La sintaxis es bastante similar al router de Angular y es fácil de migrar al UI Router.

  - Define rutas para vistas en el módulo dónde éstas existen. Cada módulo debería contener las rutas para las vistas en ese módulo.

    > ¿Por qué? Cada módulo debe ser capaz de funcionar por sí mismo.

    > ¿Por qué? Al remover un módulo o al agregar un módulo, la aplicación solo contendrá rutas que apunten a las vistas existentes.

    > ¿Por qué? Esto hace más fácil habilitar o deshabilitar porciones de una aplicación sin preocuparse de rutas huérfanas.

**[Indice](#indice)**

## Automatización de Tareas
Usa [Gulp](http://gulpjs.com) o [Grunt](http://gruntjs.com) para crear tareas automatizadas. Gulp deriva a código sobre configuración mientras que Grunt deriva a configuración sobre código. Personalmente yo prefiero Gulp ya que se siente más fácil de leer y escribir, pero ambos son excelentes.

  - Usa automatización de tareas para listar archivos que definan módulos `module.js` antes que otros archivos de JavaScript en la aplicación.

    > ¿Por qué? Angular necesita la definición de módulos para ser registrados antes de que sean usados.

    > ¿Por qué? Nombra módulos con un patrón específico como `module.js` hace más fácil tomarlos con un glob y listarlos primero.

```javascript
const CLIENTAPP = './src/client/app/'

// Siempre toma archivos de módulos primero
const files = [
    `${CLIENTAPP}**/*.module.js`,
    `${CLIENTAPP}**/*.js`
]
```

**[Indice](#indice)**