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
