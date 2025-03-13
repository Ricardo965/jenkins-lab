# Jenkins Lab

## Ejecutar Docker Compose

Para ejecutar Docker Compose, asegúrate de que tengas Docker Compose instalado en tu sistema. Luego, sigue estos pasos:

1. Navega a la ubicación donde se encuentra tu archivo `docker-compose.yml`.

2. Ejecuta el siguiente comando en tu terminal para iniciar los contenedores definidos en el archivo `docker-compose.yml`:

```bash
docker-compose up -d
```

3. Extraer passwords

```bash
docker logs id_container
```

```bash
docker exec id_container cat /var/jenkins_home/secrets/initialAdminPassword
```

Con ello, obtengo la contraseña para acceder por primera vez en Jenkins

```
docker exec 977f19207109 cat /var/jenkins_home/secrets/initialAdminPassword

```

Obtengo la siguiente salida:

`395598ca6afe491599009a71904559be`

Posteriormente, accedo a la dirección:

`localhost:8080`

Esto nos muestra la contraseña para el primer acceso y despues instalamos los plugins sugeridos junto a la creacion del primer admin para el Jenkins Controller.

Vamos a Dashboard > Manage Jenkins > Plugins y vamos a instalar el plugin nodejs.

Una vez hemos instalado el plugin, nos dirigimos a Dashboard > Manage Jenkins > Tools.

Ahora vamos a crear una herramienta de NodeJS usando el plugin que hemos instalado. Debe verse algo como esto:

![NodeTool](img/nodeTool.png)

Una vez hemos creado la tool, vamos a crear un Item de tipo Freestyle Project

![ItemCreation](img/ItemCreation.png)

Vamos a configurar el repositorio para hacer el checkout como lo siguiente:

![Repo](img/Repo.png)

Y además vamos a configurar el Environment de este Item:

![Repo](img/Env.png)

Y se configura el Build Step de tipo Execute Shell como lo siguiente para hacer que el proceso levante la app de JS y termine la ejecución dejando el servidor corriendo en background:

```
npm install
npm run build
nohup node dist/app.js &
```

Comprobación de la ejecución del pipeline y de la duración:

![Repo](img/Result.png)
![Repo](img/ResultConsole.png)
