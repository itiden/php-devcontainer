# Add a Docker devcontainer to your Wordpress project

Runs your Wordpress site in a Docker container using [Dev containers](https://code.visualstudio.com/docs/remote/containers-tutorial).  
No need to install PHP or Mysql on your computer.

This setup is done to help setup your local development environment.  
But can probably be used as a base for your production environment too with some modifications.

## Prerequisites

- Install Docker on your system (Docker Desktop for Windows and Mac)
- Install VS Code extension [Remote - Container](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Installation

In the root of your Wordpress site, run `npx degit itiden/wp-devcontainer/.devcontainer`.

This will copy the .devcontainer from this repo to your project.

Now start the containers by using the Remote - Containers extensions.

Access your site in your web browser with: [http://localhost:8080](http://localhost:8080)

Adminer (database GUI) is also istalled to access your database through: [http://localhost:8082](http://localhost:8082).

Change your database connection details in your local Wordpress site to:

```
DB_NAME=wp
DB_USER=wp
DB_PASSWORD=secret
DB_HOST=db
```

<details>
  <summary>Change web server root</summary>
  
  If the web server should not point to the root of your project.
  Change the following in your `.devcontainer/Dockerfile`:  
  `ENV APACHE_DOCUMENT_ROOT=/var/www/html/<folder>`
</details>

<details>
  <summary>Change PHP extensions, config and version</summary>

This setup uses the PHP Docker image from: [thecodingmachine/docker-images-php](https://github.com/thecodingmachine/docker-images-php).  
 Any config for PHP, Apache and Node can be change according to their setup.

Also version of PHP (default 7.4) and Node (default 14) can be changed by following their readme.

</details>

<details>
  <summary>Mysql version and access</summary>

By default Mysql 5.7 is used. This can be changed in the `.devcontainer/docker-compose.yml` file:

```
db:
  image: mysql:<version>
```

To access the database from your computer use `localhost:8081` with `user: wp, password: secret` .

</details>
