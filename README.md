# Add a Docker Dev Container to your Wordpress project

Runs your Wordpress site in a Docker container using [Dev containers](https://code.visualstudio.com/docs/remote/containers-tutorial).  
No need to install PHP or Mysql on your computer.

This setup is done to help setup your local development environment.  
But can probably be used as a base for your production environment too with some modifications (but that is currently not the intent of this repo).

## Prerequisites

- Install Docker on your system (Docker Desktop for Windows and Mac)
- Install VS Code extension [Remote - Container](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Installation

In the root of your Wordpress site, run `npx tmplr itiden/wp-devcontainer/tmplr`.  
This will prompt you with some questions where you can setup:

**project_folder**  
Name the project folder in Docker.  
(The path will be /home/wp/{{project_folder}})

**web_root**  
Select web server root  
(Relative to you repo root)

**php_version**  
Select PHP version.

**composer_version**  
Select Composer version

**node_version**  
Select Node version.

**mysql_version**
Select MySQL version.

**post_create_command**  
Command to run after entering dev container.

### Setup

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
