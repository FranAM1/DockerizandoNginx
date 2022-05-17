# DockerizandoNginx

# Instalación y prueba
Para realizar el proceso de dockerizacion de Nginx, obviamente, hace falta tener en un primer momento docker en nuestra máquina, proceso el cual explico en [este link](https://github.com/FranAM1/InstalacionDocker).

El siguiente paso seria ingresar en dockerhub y buscar la imagen de nginx.
![imagen](https://user-images.githubusercontent.com/91600940/168483065-f8de56f7-3f2e-411d-b644-dc8b0083e9a6.png)

Asi pues, ejecutamos el comando ```docker pull nginx``` para descargar la imagen. <br>
Para confirmar que la imagen se ha instalado correctamente, utilizare el siguiente comando con los siguientes parametros.
```
docker run --rm -d -p 8080:80 --name prueba nginx
```

```rm```: Se encarga de borrar automaticamente el contenedor cuando se pare. <br>
```d```: Para ejecutar el contenedor en segundo plano. <br>
```p```: Puertos del contenedor <br>
```name```: Nombre del contenedor <br> <br>
De esta forma entrando a [localhost:8080](http://localhost:8080/) nos tendria que salir la siguiente pagina confirmandonos de que todo está funcionando correctamente.
![imagen](https://user-images.githubusercontent.com/91600940/168485888-a5c402ac-8b6e-44cb-89dd-19463000a64c.png)

# HTML personalizado
Como recomiendas en el [repositorio original](https://github.com/maximofernandezriera/Ciberseguridad-PePS/blob/master/_posts/2021-01-12-nginx.md) de la guia, es recomendable crear un directorio llamado ```nginx``` y un subdirectorio dentro de este llamado ```site-content```, donde guardaremos el html personalizado.
```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Docker Nginx</title>
</head>
<body>
  <h2>Francisco José Almansa Martínez</h2>
</body>
</html>
```
Para poder utilizar este html crearemos un volumen montado, vinculando el directorio de nuestra máquina local y asignar ese directorio a nuestro contenedor en ejecución.
Ahora simplemente ejecutamos el mismo comando de antes pero añadiendo el parametro ```-v```, para crear el volumen, con su respectivia ruta. <br>
```docker run --rm -d -p 8080:80 --name web -v /home/fran/Documentos/nginx/site-content:/usr/share/nginx/html nginx```
![image](https://user-images.githubusercontent.com/91600940/168879188-5a4bf0f8-b6ab-4a37-82a6-357ce51b4ea9.png)

# Imagen personalizada
Para crear una imagen personalizada, necesitaremos crear un Dockerfile y agregarle nuestros comandos.
Para esto, crearemos un archivo llamado ```Dockerfile``` dentro de ```site-content``` para luego agregarle el siguiente comando.
```
FROM nginx:latest
COPY ./site-content/index.html /usr/share/nginx/html/index.html
```
Una vez hecho esto, para construir nuestra imagen, ejecuta el siguiente comando:
```
docker build -t webserver .
```

Para finalizar, podremos volver a hacer un docker run, pero esta vez usando la imagen que hemos creado. <br>
```docker run --rm -d -p 8080:80 --name web webserver```
![image](https://user-images.githubusercontent.com/91600940/168882555-431b5494-b4fa-4551-9f61-432a105a60cd.png)
