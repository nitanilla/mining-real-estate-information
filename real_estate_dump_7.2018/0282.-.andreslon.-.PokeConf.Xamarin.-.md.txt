# PokeConf.Xamarin

Este aplicativo fue realizado para el taller del NetConf Colombia 2017, construido en Xamarin Forms y estructurado para el primer acercamiento a DevOps.

## Objetivo

DevOps es una metodología para la creación de software que se basa en un cambio cultural para su implementación, este cambio cultural va desde la colaboración, la comunicación y la total integración entre las áreas de desarrollo y sistemas (Infraestructura).

Para este laboratorio se ha construido un aplicativo móvil llamado PokeConf el cual seguirá creciendo según necesidades del mercado, por lo que los desarrolladores deberán establecer un esquema de entrega continua ágil mediante herramientas de DevOps, en nuestro caso, se utilizara la plataforma de App center, encargada de gestionar, probar y distribuir nuestro aplicativo móvil realizado en Xamarin.

La aplicación con la que trabajaremos el taller será la siguiente, llamada PokeConf y disponible para iOS y Android.

<img src="images/-1.png" width="200">|
<img src="images/-2.png" width="200">|
<img src="images/-3.png" width="200">|
<img src="images/-4.png" width="200">
:---: |:---: |:---: |:---: |
>Pokedex

 
# App Center

App center es una plataforma creada por Microsoft que actualmente es gratis, la cual permite gestionar el desarrollo de nuestros aplicativos móviles android, ios y Windows bajo el esquema de DevOps, contando con compilación, pruebas, distribución y métricas.

### Configuración 
1. Para comenzar es necesario disponer de una cuenta en [Github](https://www.github.com).
![recursos](images/0.png)
1. Abre el repositorio donde se encuentra alojado el aplicativo prueba [Pokeconf](https://github.com/andreslon/PokeConf.Xamarin.git) y dale 
"fork" para clonar/bifurcar a tu cuenta github.
![recursos](images/0-1.png)
1. Descarga el proyecto desde tu repositorio, abrelo y recompila para restaurar los paquetes, más adelante lo necesitaremos.
![recursos](images/0-2.png)
1. Abre en el navegador la plataforma [App Center](https://appcenter.ms/apps) e inicia sesión con la cuenta Github.
![recursos](images/1.png)
1. Al ingresar correctamente, podremos darle click al botón "Add new App" para crear nuestra aplicación.
**Nota**: Se requiere crear una aplicación por cada plataforma (Android, iOS y Windows)
![recursos](images/2.png)
1. Ingresamos los datos de la aplicación, es nuestro caso este lab será bajo el sistema operativo Android y la plataforma Xamarin.
![recursos](images/3.png)
1. Ya podemos previsualizar nuestro panel general.
![recursos](images/4.png)

### Compilación (Build)

El objetivo del proceso de compilación es el siguiente, tendremos dos ramas una de desarrollo y otra de producción, la de desarrollo estará enfocada en la compilación de los cambios contantemente verificando la consistencia del código, la rama de producción además de compilar, realizará pruebas de un dispositivo físico y posteriormente distribuirá a los usuarios.

1. En el panel izquierdo ingresa a la opción **"Build"**, luego selecciona **Github** como el servicio de repositorio a utilizar.
![recursos](images/5.png)
1. El sistema se vinculará con la cuenta **Github**, luego selecciona el repositorio "Pokeconf.Xamarin" el cual fue clonado anteriormente a tu cuenta.
![recursos](images/6.png)
1. Posteriormente podrás ver las ramas de master y production.
![recursos](images/9.png) 
1. Vamos a configurar la rama master dando click en **Configure Build**, la cual es la encargada de tener todo el código correspondiente a lo que se esta desarrollando.
![recursos](images/10.png)
1. Verificamos la configuración y posteriormente guardamos y compilamos la primera vez de forma manual para verificar que todo este correcto, dando click en **Save & Build**.
![recursos](images/11.png)
1. Esperamos unos segundos a que compile y si todo esta correcto debemos ver el status **Built**
![recursos](images/11-1.png)
1. Ahora procedemos a configurar la rama de producción.
![recursos](images/12.png)
1. Debemos configurar con el objetivo de liberar la versión estable, seleccionamos configuration **Release**
![recursos](images/12-1.png) 
1. Activamos los checks: 
- **Sign Builds** para firmar las compilaciones
- **Test on a real device** para ejecutar pruebas de ejecución sobre un dispositivo real
- **Distribute builds** para luego de los pasos anteriores correctos se distribuya la aplicación a los usuarios.
![recursos](images/12-2.png) 
1. Dentro de la firma de compilaciones se nos pedirá un keystore, explora la carpeta donde descargaste el repositorio git y encontraras una carpeta llamada **keystore** y selecciona el archivo **"pokeconf.keystore"**, los datos del key son:
- keystore password: @pokeconf
- alias: pokeconf
- key password: @pokeconf
![recursos](images/12-3.png)
Luego procedemos a guardar.

- Puedes probar la compilación de forma manual, al finalizar se mostrara compilación correcta, y podrá navegar hasta la opción **Test** para verificar que la prueba en dispositivo real se haya realizado correctamente.

![recursos](images/12-4.png)
![recursos](images/12-5.png)

Las ramas que acabamos a configurar cumplen con las siguientes funciones:
- **master**: compila en todo momento que se dispara un cambio en el repositorio para verificar la consistencia de código.
- **production**: luego de que master esta estable, los desarrolladores realizaran merge a production con el objetivo de liberar versión, siendo este dentro de la metodología scrum la versión review al final de sprint.

## Crashes y Analytics

Dentro del marco DevOps es importante el tema de comunicación entre roles, de igual forma el área de desarrollo puede ser proactivo en el seguimiento de su producto ya liberado, es por eso que la plataforma de Mobile center nos brinda la opción de registrar datos de fallos o crasheos del aplicativo, además, de datos analíticos sobre su uso.

1. De forma sencilla, podemos navegar a la opción **Getting started**, en una aplicación nueva solo se requiere instalar los paquetes, pero la el ejercicio ya se encuentra configurado correctamente, solo requerimos copiar el GUID que se encuentra en:
```
MobileCenter.Start("android=c9d017a3-11c0-4af1-96e0-cd96f5f9782f;",
                   typeof(Analytics), typeof(Crashes));
```
![recursos](images/13.png)
y lo reemplazamos en nuestro aplicativo en el archivo **App.xaml.cs**
![recursos](images/13-1.png)

De esta manera ya podemos observar los crasheos que se generan en la aplicación o analizar los datos de uso.

**Nota:** En la configuración del proyecto también se puede activar la característica que envié un correo cuando exista un fallo. 

## Pruebas UI

En el proceso de DevOps uno de los pasos más importantes que asegura la calidad del producto y seguridad a cliente, son las pruebas de la aplicación en entornos reales, como sabemos existen miles variaciones de dispositivos, según marca, versión sistema operativo y características.

1. Para las pruebas de UI se requiere configurar la plataforma con el grupo de dispositivos y posterior ejecutarlas manualmente.
1. Navegamos a la opción **Test** y damos click en **New test run** para configurar las pruebas.
![recursos](images/14.png)
1. Nos solicitará seleccionar algunos dispositivos, recuerda que entre más se selecciones se demora más en ejecutar las pruebas de UI, en este caso solo seleccionamos 3 y pasamos al siguiente paso.
![recursos](images/14-1.png)
1. Creamos el test series como "master" y seleccionamos como framework de pruebas a **"Xamarin.UITest"**, seguimos al siguiente paso.
![recursos](images/14-2.png)
1. Por ultimo podemos visualizar un pequeño tutorial de como ejecutar las pruebas, y por ultimo click en **Done**.
![recursos](images/14-3.png)

A continuación realizaremos las configuraciones necesarias y ejecutaremos el código de pruebas de interfaz escritos con anterioridad.

1. Instalar Node.js, versión 6.3 o superior
1. Abrir una terminal.
1. Instalar el paquete npm mobile-center-cli con el comando: 
```
npm install -g mobile-center-cli
```
1. Es necesario autenticarnos en la terminal con el comando: 
```
mobile-center login
```
Nos abrirá el navegador indicando un código para pegar en la consola y autorizar la autenticación.
![recursos](images/32.png)
![recursos](images/31.png)
1. Por ultimo procedemos a ejecutar las pruebas de interfaz, con la configuración de dispositivos configurados.
```
mobile-center test run uitest --app "andreslon/PokeConf.App.Android" --devices "andreslon/dev1" --app-path /Users/d_p/Documents/GIT/PokeConf.Xamarin/builds/com.PokeConf.App.apk  --test-series "master" --locale "es_MX" --build-dir /Users/d_p/Documents/GIT/PokeConf.Xamarin/src/PokeConf/PokeConf.App/PokeConf.App.UITests/bin/debug
``` 
La ejecución de las pruebas puede tardar según la cantidad de dispositivos seleccionados en la plataforma.
![recursos](images/33.png)

Posteriormente puedes verificar que se hayan ejecutado correctamente los ui test.

![recursos](images/35.png)

![recursos](images/36.png)

![recursos](images/37.png)

![recursos](images/38.png) 

![recursos](images/39.png) 

## Distribución

Para finalizar, tenemos la opción de **Distribute** en la plataforma, en la cual podemos configurar grupos de usuarios para entregar las versiones compiladas automáticamente la rama de producción o también distribuir manualmente una versión firmada con el key.

![recursos](images/15.png)

![recursos](images/15-1.png)

![recursos](images/15-2.png)

![recursos](images/15-3.png)

![recursos](images/15-4.png)

## Contribución
 
Andrés Londoño - Software architect and MVP Microsoft[@Andreslon](https://twitter.com/andreslon).
 
# Comunidad Xamarin Medellín

<img src="images/XamarinMedellin.jpeg" style="height:80px;text-align:center" />

[Únete a la comunidad](https://www.meetup.com/es-ES/Xamarin-Medellin/)
