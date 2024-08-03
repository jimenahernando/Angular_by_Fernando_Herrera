# Angular

Un componente de angular cuenta con 4 partes, la unica importante y necesaria es el archivo **ts**, exceptuando un html que puede estar inline o extraerlo a un **html**
Si el archivo HTML tiene mas de 4 lineas crear un archivo aparte
Tambien existe un **css** o mas, está encapsulada y aplica a ese componente
Los archivo **spec** son relacionados al testing automatico

Angular
Es un **Framework**, un marco de trabajo estandarizado, seguimos ciertos estandares para desarrollar aplicaciones.
Angular viene con todo lo que necesitas para trabajar
Es modular, creamos modulos con objetivos especificos
Google es quien mantiene hoy en dia Angular

Bloques fundamentales:
- Componentes, bloque de codigo que tiene un html y clase de ts con decorador, se busca que sean pequeños y sencillos
- Servicios, no coupan otro gestor de estado, son singletons fuertes con informacion centralizada
- Directivas
    - De componentes, parecida a un componente con un codigo html reutilizable, conectado, con funcionalidad integrada
    - Estructurales, modifica el DOM o el html añadiendo o eliminando elementos
    - De atributos, cambian la apariencia o comportamiento de un elemento, componente u otra directiva
- Rutas, permite mostrar diferentes componenets basados en el URL del navegador web
- Modulos, permiten agrupar los anteriores y otros modulos
Se puede ver asi, por ejemplo dentro de un modulo Productos
- Componentes
- Rutas
- Directivas
- Servicios
Existen ya componentes que podemos importar, comunmente son modulos.

## Actualizacion
Desde Angular v17, por defecto los proyectos trabajan sin módulos (module-less)
Pero para trabajar de forma tradicional como lo vieron en el curso:

Para crear una aplicacion con modulos: `ng new <nombre de la aplicación> --standalone false`

Para chequear la version de angular `ng version`
Tengo instalada la 17.0.5

## 1er proyecto
Para crear el proyecto`ng new 02-bases --no-standalone`
Para arrancar la aplicacion `ng serve -o`

Antes Angular trabajaba en modulos
Ahora Angular trabaja sin modulos, con componentes standalone
Ambos son compatibles entre si, pueden mezclarse en un mismo proyecto.

## Explicacion de cada archivo del directorio
- **.editorConfig** permite sobreescribir valores por defecto, configuracion del editor
- **.gitignore** es un archivo propio de git y te permite definir que archivos van a ser ignorados al ser subidos al repositorio
- **angular.json**, de configuracion global para la ejecucion de la aplicacion
- **package-lock.json**, indica como fueron descargador los modulos de node (no se toca)
- **package.json**, propio de las aplicaciones de node, figura nombre, version, scripts, dependencias (paquetes requeridos), dependencias de desarrollo.
El ngbuild quita todo lo que no necesita pero si las dependencias
- **README.md**, es un archivo donde deberiamos explicar como luce e indicaciones para que corra la aplicacion
Angular se instala sobre node
- **tsconfig**: son archivos de configuracion de TypeScript
- **tsconfig.app.json**: son archivos de configuracion de archivos ts
- **tsconfig.spec.json**: son archivos de configuracion de archivos spec, de testing

## Directorios
- **.angular**, nunca vamos a tener que modificarlo, se genera de manera automatica y git lo ignora. Ayuda a Angular a detectar cambios, manejar cache, levantar la app
- **.vscode**,  carpeta propia del ide, que se genera automatica y que es ignorada por git
- **node_modules**, son las dependencias que necesitas para hacer correr el proyecto como nosotros no le damos manteniminento (sino sus autores) no lo subimos al repo, y lo borramos al transferirlo y con el `npm install` se vuelve a bajar
- **src**, es done creamos nuestro codigo de angular
    - favicon, icono que se muestra al lado de la pestaña de navegacion
    - index.html, tiene el <app-root>, componente personalizado donde se aloja la aplicacion
    - main.ts, punto de inicio de la aplicacion
    - style.css, donde se colocan estilos globales
    - app: carpeta donde van los componentes
        - app.component.css
        - app.component.html
        - app.component.spec.ts
        - app.component.ts -> Tiene un decorador @Component y esta definido el app-root, el componente principal y del que se desprenden todos los demas
        - app.module.ts, modulo principal
    - assets: carpeta con recursos estaticos
        .gitkeep: sirve para que git no ignore esta carpeta ya que esta vacia

## App Component

Para ver la aplicacion: `ng serve` o `npm start`
Eciste un binding entre el html y el ts
En .ts:   `public title: string = 'Mi primera app de Angular';`
En html: `<h1> {{ title }}</h1>`

Instalar en el Chrome la extension **Angular dev tools**, en el F12 en donde aparece Elements, Console.... buscar la ultima solapa de Angular
Vamos a ver que despliega el arbol de componentes y podemos ver los valores al seleccionar el componente

En el lado del html no colocar el **this.** para llamar a las funciones.
Angular esta pendiente del estado Html y lo va actualizando

## Contador Component

Como crear un componente
1. Manualmente
Creas la carpeta counter y dentro
counter.component.ts
Dentro escribimos la clase a exportar, le colocamos el decorador (importandolo de Angular core) y le definimos:
- template -> podes escribir el html o la ruta si lo extraes a un archivo html
- selector -> nombre del componente, por el cual se hace referencia en la aplicacion

Hay que agregarlo al modulo para que se pueda utilizarlo
2. Si tenemos instalada la extendion Angular Snippets poniendote en la clase escribes a- barra espaciadora y elegis component y te crea toda la estructura.
Procedemos a customizarla
Si quiero escribir todo el html en template cambiar '' por `` y te permite escribir una seccion completa en html

## Contador Hero y directorios
Cada carpeta del app/directorio será un modulo y podra vivir por si solo, de manera independiente

3. Podemos crear un componente mediante Angular CLI
cd src/app/heroes
ng g c hero
Crea un cs, html, ts, spec.ts y coloca en module este componente
Modifico el selector:   selector: 'app-heroes-hero',

Al eliminar un componente porque lo creamos en una ruta indeseada:
- Si lo hacemos un delete, nos va a dar un error porque en el modulo todavia esta definido y en el app-component se estaba utilizando

Si queremos agregar una libreria de estilos como bootstrap, entramos a su pagina 
https://getbootstrap.com/
y copiamos el link en el **index.html**
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">

Requiere recargarlo manualmente

Documentacion de interpolacion: https://v17.angular.io/guide/interpolation

## Enlazado en una sola via - One way data binding
En Angular hay que intentar cambiarlo por una sola via evitando doble via
Un get se ve como una propiedad pero en realidad es un metodo que devuelve valor
Si coloco como alcance private para un metodo/variable no es accesible desde el HTML aunque sea del mismo componente
si es public en los metodos no se escribe
en las variables poner el scope y el tipo de dato

Cuando tenemos un metodo que todavia no lo implementaremos, dejar en el codigo:
//TODO: 
o throw 'Metodo no implementado'

## *ngIf
ngIf se iguala a una expresion de Js.
true -> se ve, existe
false, 0, null, udenfined -> lo destruye

=== es para que evalue el valor y el tipo de dato

## *ngFor
Nos permite duplicar elementos, se escribe dentro del objeto html que se queire repetir

## ng-template y ngif-else
 Es un componente que no existe en el layout, que no ocupa espacio y que esta esperando que le den instrucciones para crearse

`*ngIf="deletedHeroe; else nothingWasDeleted"`
 Lo que hace es que sino se cumple la condicion lo crea (asigna nombre nothingWasDeleted)
 y en el ng-template le ponemos la referencia mediante el # -> #nothingWasDeleted
 A esto se lo conoce como referencia local

 ## Modulos en Angular
 Un modulo es una clase que tiene un decorador, es un agrupador.
 Cualquier aplicacion de angular, debe tener mas de un modulo -> varios submodulos

 Los modulos van en los imports
Con el snippet a-module te crea la estructura basica de modulo

Al separarlos en modulos, genera un error porque el *ngIf y *ngFor requieren del CommonModule. Por lo tanto, habrá que importalo en el modulo de heroes.