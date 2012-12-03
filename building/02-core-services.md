# Core Services Setup

This document covers installing services that should be useful for putting any
Web application into production.


## Git

1. Install the [Git](http://git-scm.com/) packages.

```bash
sudo apt-get install -y git git-extras git-flow
```

### Commentary

The `git-stuff` package also looked useful, but it pulled 138MB of
dependencies, so we decided against it.


## MySQL

1. Install the [MySQL](http://www.mysql.com/) packages.

```bash
sudo apt-get install -y mysql-client mysql-server libmysqlclient-dev
```

1. When the MySQL root password prompt comes up, press _Enter_ to leave the
   password blank. You might have to do this a few times.

### Commentary

We install the MySQL client to provide the `mysql` and `mysqldump` commands to
bash scripts that might use them. The development files are used by the
`mysql2` Ruby gem, and most likely by drivers in other languages.


## Nginx

1. Install the [nginx](http://nginx.org/) packages.

```bash
sudo apt-get install -y nginx nginx-full
```

1. Edit the main configuration file.

```bash
sudo vim /etc/nginx/nginx.conf
```

1. Replace `worker_processes 4` with `worker_processes 2`


### Commentary

`nginx-full` might be replaced by `nginx-extras` if there is any use for the
extra modules. Reducing the number of worker processes from 4 to 2 is
definitely the right thing to do on a unicore VM, but we're not sure if we can
further reduce it to 1.


## Tools

1. Install some commonly used tools.

```bash
sudo apt-get install -y build-essential imagemagick software-properties-common
```

### Commentary

Some of the tools installed here are used in the later steps. Some tools are
installed because they show up in many popular tutorials.

[ImageMagick](http://www.imagemagick.org/) has a strong competitor,
[GraphicsMagick](www.graphicsmagick.org). We currently ship ImageMagick because
it is used in many tutorials, and would rather not add a potential source of
bugs for students. GraphicsMagick seems to be preferred for production setups.
