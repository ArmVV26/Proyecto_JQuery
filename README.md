# Proyecto_JQuery
> [!NOTE]
> ## Descripción del Repositorio
> Este repositorio contiene el proyecto **JQuery**, desarrollado para la asignatura **Desarrollo Web en Entorno Cliente** como parte del curso de **2º DAW**.
>
> El objetivo del proyecto es desarrollar dos webs:
> - Una estilada con **TailWindCSS**, que muestra el contenido obtenido desde una *API*, con **JavaScript** normal.
> - Otra también estilada con **TailWindCSS** y mostrando el cotenido de una *API*, pero con **JQuery**.
>
> Creado por: **Armando Vaquero Vargas**

## Documentación
En este apartado se describe: la estructura del proyecto, el proceso para estilar con **TailWindCSS** y el proceso para llamar a la API. Por último, se indicará como ejecutar el proyecto y algunas capturas de este.

### 1. Estructura
El proyecto esta estructurado de la siguiente manera:
- `src/`: Directorio donde se encuentran todos los ficheros *html*, *css*, *js* y *img*. Dentro de este se encuentran los ficheros:
    - `css/`: Contiene los ficheros ***entrada.css*** y ***salida.css***.
    - `html`: Contiene los dos ficheros *html*: ***index.html*** (con el codigo **JS** normal asociado) y ***jquery.html*** (con el código **JQuery** asociado).
    - `img/`: Contiene la imagen del logotipo y una imagen para el icono de la web.
    - `js/`: Contiene los dos archivos **JavaScript**, ***pokemonAPI-JQuery.js*** y ***pokemonAPI.js***.
- ***package.json***: Archivo que centraliza la configuracion del entorno de desarrollo del proyecto y automatiza diferentes tareas.
- ***tailwind.config.css***: Archivo que configura ciertos aspectos de **TailWindCSS**, como variables o para añadir *plugin*.

### 2. Configuración de TailWindCSS
Para configurar tu web con **TailWindCSS**, es necesario hacer los siguientes pasos:

### 2.1. Configurar Node
Primero es necesario tener instalado [Node.js](https://nodejs.org/es). Una vez, comprobado que lo tenenmos instalado, nos vamos a la raiz del proyecto y inicializamos un nuevo proyecto:
```bash
npm init
```

### 2.2. Instalar TailWindCSS y Daisyui
En este proyecto, para configurar la web con **TailWindCSS**, he usado los siguientes complementos:
- [**Daisyui**](https://daisyui.com/): *Plugin* que añade una colección de componentes predefinidos.
- [**tailwindcss-bg-patterns**](https://github.com/thillmann/tailwindcss-bg-patterns): *Plugin* que proporciona utilidades para aplicar patrones de fondo.

Para instalar tanto **TailWindCSS**, como sus *plugins* se usa el siguiente comando:
```bash
npm install --save-dev tailwindcss@3 tailwindcss-bg-patterns daisyui
```

> [!WARNING]
> Existe una nueva version de **TailWindCSS**, la v.4. Lo que pasa es que esta versión cambia muchos aspectos respecto a la anterior. Por ejemplo:
> - El archivo ***tailwind.config.js***, ya no existe. Para configurar **TailWindCSS** se usa el archivo de configuracion del compilador (**Vite** o **PostCSS**) y el archivo ***CSS***.
> - En el archivo ***entrada.css***, hay que añadir solamente la línea `@import "tailwindcss";`.
> 
> Para ver los cambios que hay entre esta versión y las anteriores se pueden ver en el siguiente [enlace](https://tailwindcss.com/blog/tailwindcss-v4). 
>
> Y por otro lado, existe una nueva versión beta de **Daisyui**, la v.5, que esta si que es compatible con la versión v.4 de **TailWindCSS**.

### 2.3. Configurar TailWindCSS
Para configurar **TailWindCSS** es necesario usar el archivo de configuración ***tailwind.config.js***. Para generara este archivo es necesario usar el siguiente comando:
```bash
npx tailwindcss init
```

Esto genera un archivo básico con la siguiente estructura:
```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [],
  theme: {
    extend: {},
  },
  variants: {},
  plugins: [],
}
```

La configuracion que yo he implementado es la siguiente:
- Le indico la ubicacion de donde tiene que buscar:
```js
content: [
    './src/**/*.{html,js}',
  ],
```
- Le indico una lista de clases que simpre tiene que incluir en el CSS final:
```js
safelist: [
    'bg-pokemon-acero',
    'bg-pokemon-agua',
    'bg-pokemon-bicho',
    'bg-pokemon-dragon',
    'bg-pokemon-electrico',
    'bg-pokemon-fantasma',
    'bg-pokemon-fuego',
    'bg-pokemon-hada',
    'bg-pokemon-hielo',
    'bg-pokemon-lucha',
    'bg-pokemon-normal',
    'bg-pokemon-planta',
    'bg-pokemon-psiquico',
    'bg-pokemon-roca',
    'bg-pokemon-siniestro',
    'bg-pokemon-tierra',
    'bg-pokemon-veneno',
    'bg-pokemon-volador',
  ],
```
- Le defino también, dos fuentes, varios colores y el estilo de las sombras:
```js
theme: {
    fontFamily: {
        lato: ['Lato', 'sans-serif'],
        roboto: ['Roboto', 'sans-serif'],
    },
    extend: {
        colors: {
            'pokemon': {
                acero: '#60A1B8',
                agua: '#2980EF',
                bicho: '#91A119',
                dragon: '#5061E1',
                electrico: '#FAC000',
                fantasma: '#704170',
                fuego: '#E62829',
                hada: '#EF71EF',
                hielo: '#3FD8FF',
                lucha: '#FF8000',
                normal: '#9FA19F',
                planta: '#3FA129',
                psiquico: '#EF4179',
                roca: '#AFA981',
                siniestro: '#50413F',
                tierra: '#915121',
                veneno: '#8F41CB',
                volador: '#81B9EF',
            },
            'custom-white-red': '#FAEFEF',
            'custom-yellow': '#FFCF5F',
            'custom-black': '#312C2C',
        },
    },
    boxShadow: {
        'md': '0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1)',
        'header': '0 10px 5px 0 rgba(0, 0, 0, 0.2)',
        'footer': '0 -5px 5px 0 rgba(0, 0, 0, 0.2)',
    }
},
``` 
- También, le indico los *plugins* que voy a usar:
```js
plugins: [
    require('daisyui'),
    require('tailwindcss-bg-patterns')
],
```
- Y, por último, le modifico el color predeterminado que tiene **Daisyui**:
```js
daisyui: {
    themes: [
        {
            mytheme: {
                "primary": "#FF3B30", // Color del Header
                "secondary": "#AB2720", // Color del Footer
                "neutral": "#FAEFEF", // Hover Fondo
                "neutral-content": "#181818", // Letra Active 
                "base-content": "#FAEFEF", // Letra 
            }
        },
    ],
},
```

> Para configurar TailwindCSS es necesario usar un compilador (Vite), por que ya el fichero tailwind.config.js no existe se tiene que hacer desde el fichero vite.config.ts.
> En el CSS es donde se tiene que agregar los plugins de la empresa (daisyui)
