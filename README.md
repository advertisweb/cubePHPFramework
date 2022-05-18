# Sitio BASE - Advertis

## Índice:

* [Sobre Sitio Base](#sobre-sitio-base) 
* [Requerimientos](#requerimiento)
* [Empezando](#empezando)
* [Creenciales](#credenciales)
* [Estructura de carpetas](#estructura-de-carpetas)

* Estructura del sitio
* Configuración básica
* Levantando el proyecto con Docker
* Comandos git


## Sobre Sitio BASE
El sitio Base es el framework front-end de ADVERTIS basado en PHP, MySQL y Javascript para el desarrollo de portales y sitios de noticias.

## Requerimientos

**Requerimientos mínimos:**

- Apache
- PHP v7.2
- MySQL v5.1

**Recomendado:**

- Nginx
- PHP v7.4
- MaríaDB 10
- memcached


## Empezando
Para empezar a trabajar con **BASE** crear la carpeta del proyecto y clonar el repositorio usando `git clone http://advertis@base-v2.git/plesk-git/base-v2`. 

Para el caso de un proyecto que ya se encuentre creado, clonar el proyecto por ejemplo: `git clone http://advertis@advertis.com.ar.git/plesk-git/advertis.com.ar`.


En la terminal posicionarse en la carpeta del proyecto y ejecutar el siguiente comando para levantar el contenedor docker.
> Es necesario que tengas Docker previamente instalado. Podes instalarlo desde https://www.docker.com/get-started/ 
```bash
> docker-compose up -d
```

Esto levanta el sitio en http://localhost utilizando Nginx, PHP y MySQL.

Para acceder al PHPMyAdmin ingresa a http://localhost:8088 

El sitio ya posee algunos parámetros básicos y contenido de prueba que permiten tener un sitio 100% funcional.


### Credenciales

Variables para conectar a la base de datos:
* Host: `$SS['db_host']`
* Database Name: `$SS['db_name']`
* Username: `$SS['db_user']`
* Password: `$SS['db_pass']`

Estas variables se encuentran en el archivo `datasite.php` para el modo producción y en `datasite-local.php` para el modo desarrollo.

Estos archivos se encuentran en la ruta: 
```html
/includes/site/config/
```


### Estructura de carpetas

Todos los sitios de `ADVERTIS` tienen una estructura de carpetas similar a la siguiente:

```
.
├── debug
├── docker
├── errodocs
├── extras
│   ├── crons
│   ├── descargas
│   ├── encuestas
│   ├── js
│   ├── newsletter
│   ├── notas
│   └── vivo
├── galeria
├── images
├── includes
│   ├── app
│   │   ├── classes
│   │   ├── config
│   │   ├── controllers
│   │   ├── helpers
│   │   ├── libs
│   │   │   ├── db
│   │   │   ├── mails
│   │   │   ├── parts
│   │   │   └── upload
│   │   ├── snippet
│   │   │   └── header
│   │   └── vars
│   ├── cache
│   ├── crons
│   ├── site
│   │   ├── classes
│   │   ├── config
│   │   ├── controllers
│   │   ├── crons
│   │   ├── helpers
│   │   └── templates
│   │       ├── amp
│   │       ├── common
│   │       ├── components
│   │       ├── emails
│   │       ├── errors
│   │       ├── home
│   │       ├── news
│   │       ├── pages
│   │       └── widgets
│   └── tmp
├── js
├── pages
├── styles
└── unit-test
```

### 3. URLs del sitio

Los sitios de advertis poseen esta estructura de URLs que se complementa con las particulares de cada sitio.

| URL                           | Método    | Descripción       |
| -----------------             | ----------------- | ----------------- | 
| /ads.txt                      | GET       | Archivo con información para gestión de anuncios |
| /amp/([a-z0-9_-]+).htm        | GET       | Páginas AMP. Versión AMP de las notas |
| /buscador                     | GET       | Página para resultados del buscador. Los Parámetros de búsqueda son con query string |
| /clima/?([0-9]+)              | GET       | Página que muestra el clima, si se posee el primer parámetro, muestra el clima de la localidad solicitada. En caso contrario muestra el clima de la localidad por defecto. |
| /extras/crons/index.php       | GET       | Página para ejecutar los Crons del sitio |
| /extras/crons/logs.php        | GET       | Página para vsicualizar los logs del Crons consultado |
| /extras/descargas/descarga.php | GET  | Página para descargar las imagenes o archivos adjuntos a las notas |
| /extras/encuestas/votar.php   | POST    | Carga la votación a algún item de la encuesta |
| /extras/js/clima.php          | GET | Devuelve información del clima de todas las localidades definidas |
| /extras/newsletter/index.php  | POST   | Guarda los datos del usuario ( email ) para recibir newsletter |
| /extras/notas/comentarios.php | GET   | Recupera información de los comentarios de la nota |
| /extras/notas/comentarios-enviar.php | POST | Guarda información del comentario para una nota en particular |
| /extras/notas/enviar.php      | GET POST  | Página para enviar nota vía email ( recomendar notas ) |
| /extras/notas/reporte.php     | POST      | Envía una denuncia sobre un comentario en particular |
| /extras/notas/voto.php        | POST      | Envía un voto ( positivo o negativo ) sobre una nota en particular |
| /extras/publicidad.php        | POST      | Se le envía información de los banners que se estan mostrando y los clicks que tengan |
| /extras/vivo/ajax.php         | GET       | Muestra información sobre un video a mostrar en alguna parte del sitio |
| /extras/vivo/sse.php          | GET       | Muestra información sobre un video a mostrar en alguna parte del sitio |
| /galeria/(*.)/([0-9]+)/([0-9]+)/([0-9]+)/(*.) | GET | En el caso de que la imagen o la versión de la foto ( original, thumbnail, large, etc ) no exista, intenta recuperar información de la imagen origianl y muestra la versión solicitada. |
| /js/search.xml                | GET       | Página con información para el navegador. Le indica como debe buscar en el sitio cuando escribis la URL |
| /robots.txt                   | GET       | Información de robots.txt |
| /rss/feed.xml                 | GET       | Página para mostrar el RSS de las últimas notas |
| /sitemap.xml                  | GET       | Página para mostrar el mapa de notas para Google Search Console |
| /sitemap_lite.xml             | GET       | Página para mostrar el mapa de notas para Google Search Console |
| /sitemap-news.xml             | GET       | Página para mostrar listado de notas para Google News |
| /temas/?([a-z0-9_-]+)?/?([0-9]+) | GET | Listado de notas agrupadas por etiquetas. La primer variable es la etiqueta, la segunda variable hace referencia a la paginación |
| /uid-([0-9]+)(\-(.+))         | GET       | Acortador. la primer variable le indica el ID de la nota, la segunda es un set de caracteres de control en el caso que pa nota no se encuentre publicada y deba mostrarse |
| /([a-z0-9_-]+)/([a-z0-9_-]+).htm | GET | Artículo. La primer variable indica el nombre de la sección de la nota, la segunda variable indica el slug del artículo. | 
| /([a-z0-9_-]+)?/?([0-9]+)     | GET       | Listado de Artículos. La primer variable indica el nombre de la sección de la nota, la segunda  variable (opcional) indica la página a visualizar. | 
| /([0-9]+)/([0-9]+)/([0-9]+)/(.+)/ | GET | Wordpress migration. El último parámetro es el slug del artículo, con esta info redirecciona con 301 a /seccion/slug.htm Ej: /2022/03/21/nota-de-prueba/ >> /policiales/nota-de-prueba.htm  |
| /([0-9]+)/([0-9]+)/(.+)/      | GET       | Wordpress migration. El último parámetro es el slug del artículo, con esta info redirecciona con 301 a /seccion/slug.htm Ej: /2022/03/nota-de-prueba/ >> /policiales/nota-de-prueba.htm |
| /category/(.*)                | GET       | Wordpress migration. El parámetro es el slug de la seccion. Con esto redirecciona con 301 a la seccion correspondiente. Ej: /category/policiales > /policiales |


#### 3.1 Expresiones regulares de las URLs

```html
/amp/([a-z0-9_-]+).htm
```
| Parametro | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `match[1]` | `string` | Slug de la nota. |


```html
/clima/?([0-9]+)
```
| Parametro | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `match[1]` | `integer` | **(Opcional)** ID del clima. Este valor corresponde al ID del clima de Yahoo Wheater y debe estar previamente declarado en el archivo `datasite.php` |

```html
/galeria/(*.)/([0-9]+)/([0-9]+)/([0-9]+)/(*.)
```
| Parametro | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `match[1]` | `string` | Carpeta de la galería. Puede ser cualquiera de las carpetas, ej: `fotos`, `fotos-autor`, etc |
| `match[2]` | `integer` | Año expresado en 4 dígitos para la subida de la imagen o archivo. |
| `match[3]` | `integer` | Mes expresado en 2 dígitos para la subida de la imagen o archivo. |
| `match[4]` | `integer` | Día expresado en 2 dígitos para la subida de la imagen o archivo. |
| `match[5]` | `string` | Nombre del archivo tal como aparece en la base de datos con el prefijo o sufijo para indicar la versión ( en el caso de imagen la versión thumnails, large, etc). |


```html
/temas/?([a-z0-9_-]+)?/?([0-9]+)
```
| Parametro | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `match[1]` | `string` | Slug de la etiqueta. En el caso que se omita este parámetro o no exista redirecciona con 301 al home |
| `match[2]` | `integer` | **(Opcional)** Número de la página a retornar. Si se omite devuelve la página inicial ( página cero ) |

```html
/uid-([0-9]+)(\-(.+))
```
| Parametro | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `match[1]` | `integer` | ID de la nota. en el caso de que sea un ID válido redirecciona con 301 a la URL del artículo. |
| `match[2]` | `string` | **(Opcional)** Hash para validar la visualización de un artículo que no está público ( se encuentra en borrador o programado ). |

```html
/([a-z0-9_-]+)/([a-z0-9_-]+).htm
```
| Parametro | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `match[1]` | `string` | Slug de la sección del artículo. |
| `match[2]` | `string` | Slug del artículo. |

```html
/([a-z0-9_-]+)?/?([0-9]+)
```
| Parametro | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `match[1]` | `string` | Slug de la sección de artículos. |
| `match[2]` | `integer` | **(Opcional)** Número de la página a retornar. Si se omite devuelve la página inicial ( página cero ) |




#### 3.2 Variables GET o POST en las URLs

```html
/buscador
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `q` `GET` | `string` | Texto de la búsqueda. |


```html
/extras/descargas/descarga.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `id` `GET` | `integer` | ID del objeto multimedia a descagrar ( imagenes, audios, documentos ). |


```html
/extras/encuestas/votar.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `enc` `POST` | `integer` | ID de la encuesta a votar ( debe estar activa ) |
| `id` `POST` | `integer` | ID del Item a votar |

```html
/extras/newsletter/index.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `email` `POST` | `string` | Email de la parsona a registrar al newsletter |
| `nombre` `POST` | `string` | **(Opcional)** Nombre de la parsona a registrar al newsletter |

```html
/extras/notas/comentarios.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `id` `GET` | `integer` | ID del artículo a consultar por comentarios. Devuelve la totalidad de comentarios aprobados para el artículo. |

```html
/extras/notas/comentarios-enviar.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `id` `POST` | `integer` | ID del artículo a consultar por comentarios. Devuelve la totalidad de comentarios aprobados para el artículo. |
| `nombre` `POST` | `string` | Nombre del usuario |
| `email` `POST` | `string` | Email del usuario |
| `comentario` `POST` | `string` | Comentario del usuario |


```html
/extras/notas/enviar.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `id` `GET` | `integer` | ID del artículo a consultar por comentarios. Devuelve la totalidad de comentarios aprobados para el artículo. |
| `nombre` `POST` | `string` | Nombre del usuario que envía la recomendación|
| `email` `POST` | `string` | Email del usuario que envía la recomendación|
| `destinatario` `POST` | `string` | Nombre de la persona que recibe la recomendación|
| `destinatario-email` `POST` | `string` | Email de la persona que recibe la recomendación|
| `comentario` `POST` | `string` | **(Opcional)** Comentario que en envía al recomendar una nota |


```html
/extras/notas/reporte.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `id` `GET` | `integer` | ID del artículo. |
| `com` `GET` | `integer` | ID del comentario a reportar. |


```html
/extras/notas/voto.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `id` `GET` | `integer` | ID del artículo. |
| `com` `GET` | `integer` | ID del comentario a realizar el voto. |
| `vt` `GET` | `integer` | Valoración del comentario (0: negativo / 1:positivo). |


```html
/extras/publicidad.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `id` `POST` | `integer` `string` | En el caso de que sea un solo ID indica que es un click. En el caso de que sea un string, son varios IDs separados por coma y se guarda como impresión de banners |


```html
/([a-z0-9_-]+)/([a-z0-9_-]+).htm
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `mid` `GET` | `string` | **(Opcional)** Flag utilizado para mostrar artículos que esten en modo borrador o programados. |


```html
/extras/crons/index.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `fl` `GET` | `string` | Flag utilizado para indicar el cron a ejecutar. |


```html
extras/crons/logs.php
```
| Variable | Tipo     | Descripción                |
| :-------- | :------- | :------------------------- |
| `fl` `GET` | `string` | Flag utilizado para indicar el cron que queremos ver el log. |

### 4. Uso de los templates

Cada página está compuesta por la siguiente estructura del sitio. que puede llamar o no a los siguiente archivos.

```
┌────────────────────────────────────────────────┐
│ header                                         │
│  - header.php                                  │
│  - top.php                                     │
├─────────────┬───────────────────┬──────────────┤
│ left        │ body              │ right        │
│  - left.php │  - interior.php   │  - right.php │
│             │    / listado.php  │              │
├─────────────┴───────────────────┴──────────────┤
│ bottom                                         │
│  - pie.php                                     │
│  - bottom.php                                  │
└────────────────────────────────────────────────┘
```
