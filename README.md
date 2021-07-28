# Add a Docker Dev Container to your Wordpress project

Runs your Wordpress site in a Docker container using [Dev containers](https://code.visualstudio.com/docs/remote/containers-tutorial).  
No need to install PHP or Mysql on your computer.

This setup is done to help setup your local development environment.  
But can probably be used as a base for your production environment too with some modifications (but that is currently not the intent of this repo).

## Prerequisites

- Install Docker on your system (Docker Desktop for Windows and Mac)
- Install VS Code extension [Remote - Container](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Installation

In the root of your Wordpress site, run `npx degit itiden/wp-devcontainer/.devcontainer#main .devcontainer`.  
This will copy the .devcontainer from this repo to your project.

Change your database connection details in your local Wordpress site to:

```
DB_NAME=wp
DB_USER=wp
DB_PASSWORD=secret
DB_HOST=db
```

Now start the containers by using the Remote - Containers extensions.

- Access your site in your web browser: [http://localhost:8080](http://localhost:8080)
- Adminer (database GUI) accessed through: [http://localhost:8082](http://localhost:8082).

<details>
  <summary>Change web server root</summary>

#### Default the webroot is the project root

If the web server should not point to the root of your project.
Change the following in your `.devcontainer/docker-compose.yml`:  
 `APACHE_DOCUMENT_ROOT: /var/www/html/<folder>`

</details>

<details>
  <summary>Change PHP extensions, config and version</summary>

#### Default PHP version is 8.0 with Apache and Node 14

This setup uses the PHP Docker image from: [thecodingmachine/docker-images-php](https://github.com/thecodingmachine/docker-images-php).  
Any config for PHP, Apache and Node can be change according to their setup.

Also version of PHP and Node can be changed by following their readme.

</details>

<details>
  <summary>Mysql version and access</summary>

#### By default Mysql 8.0 is used.

This can be changed in the `.devcontainer/docker-compose.yml` file:

```
db:
  image: mysql:<version>
```

To access the database from your computer use `localhost:8081` with `user: wp, password: secret` .

</details>
