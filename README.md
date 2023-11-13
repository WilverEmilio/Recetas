![image](https://github.com/WilverEmilio/Recetas/assets/125522983/aefd332d-7c9e-4fe2-89fd-d0b79388b8f9)# Recetas
Es un proyecto de programacion web juntamente con arquitectura de sistemas basado en recetas

cosas por tener instaladas
- mysql
- xampp
- npm
- composer
Nota: mysql y composer vienen juntamente con xampp

#Pasos para la instalación
crear una carpeta llamada recetas en cualquier lado, preferiblemente en donde se encuentra instalado xampp y en la carpeta de htdocs 
1. Clonar el repositorio
2. Ver si te se tiene composer, php y mysql en las variables de entorno
3. Si no estan esas variables ponerlas ![image](https://github.com/WilverEmilio/Recetas/assets/125522983/7cdda57d-58b7-417c-94fa-e843333fe4ec)
4. En el git clonado ir a la carpeta api y poder el comando composer install
5. En la misma carpeta api crear un nuevo archivo env.php y guiarse del env.ejemplo.php (solo copiar y pegar el codigo)
6. Crear una carpeta llamada fotos_recetas
7. Crear la base de datos en mysql se tiene que llamar recetas (el scrip lo pueden encontrar en la carpeta api y se llama esquema)
8. Regresar a la carpeta principal
9. Entrar a la consola y poder npm install
10. Esto creara una carpeta node_modules debajo de api
11. Ir al archivo .env
12. Poner la siguiente ruta VUE_APP_RUTA_API=http://localhost/recetas/api
13. Ir en el archivo .env.production y poner VUE_APP_RUTA_API=http://localhost/recetas/api
14. Teniendo todo esto ya se puede ejecutar con npm run serve

Nota: Para crear la base de datos hay doa maneras, directamente desde el mysql
y la segunda es ir a la consola y poner mysql -u root -p ![image](https://github.com/WilverEmilio/Recetas/assets/125522983/58dbdfa2-18b8-42ff-a99d-7b9d8681533d)
poner create database recetas (crear la base de datos)
use recetas (utilizar esa base de datos)
pegar el script de las tablas 
poner show Tables; (visualizar todas las tablas que tiene) ![image](https://github.com/WilverEmilio/Recetas/assets/125522983/e45316e3-e651-4941-be52-59d4779f54fc)
