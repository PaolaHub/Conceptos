
# SEO y Posicionamiento web para Desarrolladores web

# ¿ Qué es el SEO ?

Search Engine Optimización (Optimización para motores de busquedad)
Son las técnicas que nos permiten mejorar la optimización de nuestros sitios web
para tener mejores posiciones en los buscadores de Internet de manera orgánica
**Organico** (que no has pagado nada para posicionarlo)
y acercarnos lo máximo posible a la primera posición. Que cuando alguien busque
nuestra web, blog, la encuentre fácilmente y así pueda consumir nuesro contenido
o comprar productos.

# Ventajas y desventajas del SEO

Lo bueno...

1. Es gratuito
2. El posicionamiento orgánico es muy efectvo. Porque pertenece más en el tiempo y
porque la gente que lo consuma es porque lo ha buscado y lo ha encontrado.
3. Impactar con contenidos. Subir contenidos frecuentemente, así aumentas
el tráfico de tu página y la página se vuelve más visible.
4. Impactar satisfaciendo la intención de búsqueda. Por ejemplo un chico que quiere
comprar unas deportivas, y tu haces un contenido de las 10 deportivas más buenas del 2020.
Le estás dando información de la busquedad y aparte si pones algún link, de donde
quiere comprarlo, estás satisfaciendo su objetivo de busqueda.

Lo malo...

1. No es inmediato. Igual no se posiciona de aquí a dos meses.
No se puede prometer dentro del SEO que vaya aparecer en el puesto numero uno.
El SEO es a largo plazo.
2. No hay píldoras mágicas, solo trabajo. Nadie puede garantizar que puedas aparecer el primero en Google.
Porque los algorithmos tiene en cuenta muchas cosas.
3. No se puede garantizar el éxito. Competencia, si una página tiene una alta competencia, le va ser más dificil que
se posicione, porque ya la otra página está bien posicionada.

# ¿Que es el SEM?

Son campañas de pago.
Para potenciar junto al SEO la visibilidad de nuestra web.
Search Engine Marketing. Nos permite atraer tráfico (visitantes) a nuestro sitios web mediante
campañas de marketing o publicitarias de pago.

La diferencia
El SEO es orgánico.
El SEM es inmediato, si tu pagas vas aparecer el primero, pero si dejas de pagar
ya no aparecer ahí en el buscador. Si no lo complementas con una campaña de SEO positiva
pues ese dinero que invertimos va ser pan para hoy y agua para mañana.

El SEM es mucho más rápido que el SEO. Pero mucho menos efectivo que el posicionamiento orgánico.
El SEO es más afevtivo a largo plazo.

# Que cosas no se pueden prometer en SEO

El SEO real.
Aparecer el primero en la página de resultados de Google(SERPs) (o un buscador).
En pocos días aparacerás de los primeros.
Alto volumen de visitas.
Aparecer delante de los competidores.
Todo rápido sin contenido.
Quien te prometa esto te está engañando.
Puedes caer en penalizaciones por malas practicas.

# SEO On-Page

### HTML para SEO

- Importante para el desarrollo del sitio web.
- Importante para la redacción de textos (copywriting).
- Buena semántica HTML5 (usar bien las etiquetas ya de html, va ayudar a Google
a leer mejor la web y lo va posicionar mejor porque la va a indexar mucho mejor)
**(indexar es que Google nos lee la web y nos la posicione en el buscador)**
- Etiqueta title <title>
- Etiquetas <meta> -title, description, keywords y robots
- Jerarquía de < h1 > (único) < h2 >< h3...6 > (muchos)
- Párrafos <p> y listas <ul><ol>
- Negritas <strong> (sin pasarnos)
- Enlaces - Atributo nofollow en links no relevantes.
  El addschortext (texto que hay dentro de un enlace). Poner ahí una palabra clave
  Pero interesante en definirle el atributo **nofollow**, para deirle que no lo indexe.
  Por ejemplo poner un enlace de un producto de amazon que realmente no está en tu web
  y no quieres que se indexe, pues definirle el atributo nofollow.
- Enlaces - Atributo rel="canonical" para el link más relevante y tenga cierto peso
  para indexarlo.
- Enlaces con atributo title. Y en ese title poner la palabra clave del articulo al que apunta.
- Enlaces con texto relevante (titulo)
- Imágenes con atributo ALT. y tambien el titulo.
- Imágenes con nombre descriptivo y con tamaño reducido. (compressor.io o compresspng.com)
- Reduce al mínimo el código en línea y spaghetti.

### Optimización del sitio web

Mejorar la velocidad de las webs.
- Google analitycs (head) y search console configurado. Herramienta interesante para ver que cosas
está funcionando en nuestra web. Hay que registrarse y nos da un código que tenemos que poner en el head.
- URLs limpias y amigables.
- URLs cuanto más cortas y concretas. Ajustada a la palabra clave.
- Sitio web rápido (más adelante).
- Responsive web design.
- robots.txt (manual). Es un achivo que le indica a Google que queremos que indexe y que no.
  Ejemplo de un archivo robots.txt (https://www.genbeta.com/robots.txt)

        #
        # robots.txt
        #

        # First, this is the
        # robots.txt from http://www.wikipedia.org/ for "other" robots
        # Thanks Wikipedians!
        #
        # Please note: There are a lot of pages on this site, and there are
        # some misbehaved spiders out there that go _way_ too fast. If you're
        # irresponsible, your access to the site may be blocked.
        #
        #User-agent: Mediapartners-Google*
        #Disallow:

        User-agent: Orthogaffe
        Disallow: /

        # Crawlers that are kind enough to obey, but which we'd rather not have
        # unless they're feeding search engines.
        User-agent: UbiCrawler
        Disallow: /

        User-agent: DOC
        Disallow: /

        User-agent: Zao
        Disallow: /

        User-agent: gsa-crawler
        Disallow: /

        # Some bots are known to be trouble, particularly those designed to copy
        # entire sites. Please obey robots.txt.
        User-agent: sitecheck.internetseer.com
        Disallow: /

        User-agent: Zealbot
        Disallow: /

        User-agent: MSIECrawler
        Disallow: /

        User-agent: SiteSnagger
        Disallow: /

        User-agent: WebStripper
        Disallow: /

        User-agent: WebCopier
        Disallow: /

        User-agent: Fetch
        Disallow: /

        User-agent: Offline Explorer
        Disallow: /

        User-agent: Teleport
        Disallow: /

        User-agent: TeleportPro
        Disallow: /

        User-agent: WebZIP
        Disallow: /

        User-agent: linko
        Disallow: /

        User-agent: HTTrack
        Disallow: /

        User-agent: Microsoft.URL.Control
        Disallow: /

        User-agent: Xenu
        Disallow: /

        User-agent: larbin
        Disallow: /

        User-agent: libwww
        Disallow: /

        User-agent: ZyBORG
        Disallow: /

        User-agent: Download Ninja
        Disallow: /

        # Sorry, wget in its recursive mode is a frequent problem.
        # Please read the man page and use it properly; there is a
        # --wait option you can use to set the delay between hits,
        # for instance.
        #
        User-agent: wget
        Disallow: /

        #
        # The 'grub' distributed client has been *very* poorly behaved.
        #
        User-agent: grub-client
        Disallow: /

        #
        # Doesn't follow robots.txt anyway, but...
        #
        User-agent: k2spider
        Disallow: /

        #
        # Hits many times per second, not acceptable
        # http://www.nameprotect.com/botinfo.html
        User-agent: NPBot
        Disallow: /

        # A capture bot, downloads gazillions of pages with no public benefit
        # http://www.webreaper.net/
        User-agent: WebReaper
        Disallow: /

        User-agent: CNCDialer
        Disallow: /

        User-agent: Maxthon
        Disallow: /

        User-agent: MJ12bot
        Disallow: /

        User-agent: Slurp
        Disallow: /

        User-agent: Screaming Frog SEO Spider
        Disallow: /

        User-agent: *
        Allow: /.well-known/*
        Disallow: /wp-content/
        Disallow: /wp-admin/
        Disallow: /wp-includes/
        Disallow: /wpi/
        Disallow: /trackback/
        Disallow: /*/*/*/feed.xml
        Allow: /retro/*
        Disallow: /retro
        Disallow: /login.php/
        Disallow: /frontend.php/
        Disallow: /api/1.0/migration
        Disallow: /server
        Disallow: /queue
        Disallow: /mobile.php/
        Disallow: /app.php/
        Disallow: /main.php/
        Disallow: /redirect
        Disallow: /approve
        Disallow: /duplicate
        Disallow: /1018282
        Disallow: /api/
        Disallow: /c/
        Disallow: /morepostcomments
        Disallow: /offtopic
        Disallow: /p/
        Disallow: /pda
        Disallow: /tracker

        Sitemap: https://www.genbeta.com/sitemap_news.xml
        Sitemap: https://www.genbeta.com/club/sitemap.xml
        Sitemap: https://www.genbeta.com/sitemap_index.xml
        Sitemap: https://www.genbeta.com/2019/sitemap_galleries.xml
        Sitemap: https://www.genbeta.com/2018/sitemap_galleries.xml
        Sitemap: https://www.genbeta.com/2017/sitemap_galleries.xml
        Sitemap: https://www.genbeta.com/2016/sitemap_galleries.xml
        Sitemap: https://www.genbeta.com/2015/sitemap_galleries.xml
        
- Sitemap.xml (Se pueden generar instalando plugins o con xml-sitemaps.com)
  El sitemap tiene todas las urls de nuestra web.
- Subir sitemap a Google (mediante el search console). Lo podemos tener en nuestra web generado en la raiz del proyecto.
  Podemos directamente subir el archivo a Google mediante el search console, así a la hora de indexer lo va hacer mucho más
  rápido y por ellos nos colocará mucho más arriba.
- No hay URLs que lleven a ningún sitio (404). ¿Como podemos ver que nuestras página tiene urls 404?
- Redirecciones 301 (.htaccess) En el archivo escribimos las redirecciones y ese archivo lo encontramos en el directorio principal         también. (Redirect 301 /Blog /blog). Blog sería la página 404 y e blog sería la página a la que direccionamos.
- Añadir rel="prev" y rel="next" en paginaciones (no tan importante)
- HTTPs activado. Tener activado el sistema HTTP de seguridad. Si no lo tenemos Google, nos va a penalizar.
  Normalmente, en los hosting ya viene incluido y no tener que hacer mucho. Se puede redirigir las peticiones http a un https con un        plugings.
- Dominio global. Si quieres llegar a todo el mundo es importante que uses un dominio global. (.com / .net / .org)
- Fácil navegación en el sitio (menús, breadcrumbs, sidebar con enlaces internos).
- Página 404 útil. Siempre las mínimas posibles, pero si necesitamos alguna, que tenga documentación dentro para que pueda redirigirse
  o algo para que no quede tan vacia.

### Contenido

Palabras claves.
Búsqueda de palabras clave.
Lo importate: el contenido.
Optimizar el contenido.
Como crear contenido de calidad.

### Conseguir más trafico

### Motivos de penalización

### Cosas que perjudican al SEO







# SEO Off-Page

# Como indexar webs

# Factores extra para posicionamiento web

# SEO Práctico

# Posicionarte en los buscadores y tener + visitas
