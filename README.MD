![Plenco](https://cdn.plen.co/plencovich.png)

# Github Actions Workflows

## PHP - COMPOSER - NPM - RSYNC - AUTODEPLOY

### Ejemplo usando rsync

Utilizando el ejemplo [rsync-example.yaml](/workflows/rsync-example.yml) se puede realizar un deploy automático utilizando:

- Instalación de las dependencias de composer.json
- Instalación de los paquetes de Node.js
- Generar el build de npm
- Sincronizar a un servidor los archivos de producción utilizando el comando `rsync` y accediendo por SSH; se usará un archivo `exclude.txt` que contiene los archivos a excluir del `rsync`

Dentro de las configuraciones del repositorio, se deberá agregar las variables de entorno en **secrets**. Las utilizadas en este ejemplo son:

- PROD_HOST: Nombre del host del servidor `server.mydomain.com`
- PROD_FOLDER: Nombre de la ruta absoluta donde deben estar los archivos a copiar `/home/mydomain/public_html/`
- PROD_USER: Usuario que tiene acceso por SSH
- SSH_KEY: Clave privada generada para conectar con el servidor; la clave pública debe estar en el archivo `authorized_keys` del servidor. [¿Cómo generar una clave SSH?](https://docs.github.com/es/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

### Ejemplo usando autodeploy con git

Utilizando el ejemplo [autodeploy-example.yaml](/workflows/autodeploy-example.yml) se puede realizar un deploy automático utilizando:

- Instalación de las dependencias de composer.json
- Instalación de los paquetes de Node.js
- Generar el build de npm
- Generar una rama que contiene el contenido exclusivo que se hará el deploy en producción; la clave está en tener un archivo `.deployignore` donde indicaremos ahí todos los archivos que deben ser ignorados en la rama **master-build**

Para un deploy automático, luego dentro de la configuración del repositorio en **Webhooks** debemos configurar la acción a realizar para que en el servidor se ejecute el `git pull ...`; en muchos servidores con cPanel, CentOs Web Panel, [Cloudways](https://vrlps.co/LmAt0bY/cp), [DigitalOcean](https://m.do.co/c/1b7ae0ce9fb9) u otros servicios de hosting/paneles; tienen la opción para conectar un repositorio para poder hacer el **Deploy via Git**
