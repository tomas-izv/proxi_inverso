# Proxy inverso

El código de Vagrant para el despliegue sería el siguiente:
<a href="./Vagrantfile"></a>

<img src="./imgs/vagrantfile.png" alt="Vagrantfile">

## Configuraremos el servidor *w1* con los siguientes pasos:

### w1

1. `/etc/nginx/sites-available/default`
2. `sudo systemctl restart nginx`
3. `/var/www/html/index.html`
4. `sudo apt install -y curl`
5. <img src="./imgs/curl_web.pmng" alt="Curl w1">
   
## Nginx *proxy* inverso

### proxy

1. `/etc/hosts`  
<img src="./imgs/default_proxy.png" alt="First Proxy Default">
2. `sudo systemctl restart nginx`

3. <img src="./imgs/proxy_w1.png" alt="Curl proxy">

## Logs

1. Accederemos en nuestro navegador a la dirección 192.168.57.10
<img src="./imgs/1921685710.png" alt="Page">
2. Accederemos a los logs de proxy
`sudo tail /var/log/nginx/access.log`
<img src="./imgs/tail_proxy.png" alt="Tail Proxy">
3. Accederemos a los logs de web
`sudo tail /var/log/nginx/access.log`
<img src="./imgs/tail_w1.png" alt="Tail Web">

## Cabeceras

1. En Firefox pulsaremos Ctrl+Shift+I u opciones / more tools / Web developer tools. Luego pulsaremos en Network y marcaremos Disable cache.
2. Recargaremos la página y examinaremos la petición (en rojo) dónde se puede ver la respuesta GET HTTP (200 OK)
<img src="./imgs/cabecera10.png" alt="Cabecera">
3. Usando DNS
Si accedemos mediante un nombre de host www.192.168.57.10.nip.io, veremos que la cabecera Host cambia. Pruebalo.
<img src="./imgs/cabecera_10_dns.png" alt="Cabecera DNS">


## Añadiendo Cabeceras

1. Para añadir cabeceras, en el archivo de configuración del sitio web de proxy debemos añadir dentro del bloque location / { … } debemos añadir la directiva:
<img src="./imgs/default_proxy_1.png" alt="Default Proxy 1">
2. `sudo systemctl restart nginx` 
3. Con las herramientas de desarrollador comprobamos que la petición ha pasado por el proxy inverso que ha añadido la cabecera en la respuesta.
<img src="./imgs/cabecera_10_tomas.png" alt="Cabecera tomas">

## Cabeceras en el servidor web

1. Añadiremos también una cabecera en el servidor web:
`/etc/nginx/sites-enabled/default de web`
<img src="./imgs/default_w1_1.png" alt="Default w1 1">
2. `sudo systemctl restart nginx` 
3. <img src="./imgs/cabecera_10_host.png" alt="Cabecera host">

## Ampliación








