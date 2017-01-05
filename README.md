# How to create a repository debian


#### First install dependencies:


>
```bash
$ sudo apt install reprepo apache2 gnupg
```

#### Generate the key gpg to firm the packages

>
```bash
$ sudo gpg --gen-key  
```

#### Check the key created

>
```bash
$ sudo gpg --list-keys 
```

#### Now Create the struct the repo

>
```bash
$ sudo mkdir -p /var/www/html/repositorio/conf
```

#### A the directory 

>
```bash
$ cd /var/www/html/repositorio/conf
```


#### Create the file ```distributions```


>
```bash
$ sudo vim distributions
```

With the following info:


* Origin: Name of the distribution.
* Label: Etiqueta de la distribución o sabor. Generalmente se utiliza el mismo valor de Origin.
* Codename: Nombre código de la distribución o sabor (p. ej: aponwao, roraima, auyantepui).
* Suite: Nombre del estado de desarrollo de la distribución (p. ej: estable, pruebas, desarrollo).
* Version: Versión de la distribución o sabor.
* Pull: Distribución desde donde se actualizan los paquetes.
* Description: Descripción de la distribución.
* Architectures: Arquitecturas soportadas por la distribución o sabor.
* Components: Componentes o secciones en las que se divide el repositorio (p. ej: main, contrib, non-free).
* SignWith: Código de la Llave pública GPG o correo asociado con que se firma el repositorio.
* DebIndices: Tipos de Índices a generar.


Debes agregar un bloque de éstos por cada estado de desarrollo de la distribución. Por ejemplo, el archivo conf/distributions del repositorio de Canaima para 3.0 es el siguiente:


>
```bash
Origin: Gescolar
Label: Gescolar
Suite: stable
Codename: jessie
Version: 8.0
Pull: estable
Architectures: i386 amd64 source
Components: usuarios
Description: Repositorio gescolar
SignWith: 5F01BE71
DebIndices: Packages Release . .gz .bz2
```

In the field SignWith put the ID that give us the command sudo ```gpg --list-keys```

```bash
pub   2048R/```5F01BE71``` 2017-01-05
uid                  Victor Pino <victopin0@gmail.com>
```

#### Export the key gpg

>
```bash
$ sudo gpg --armor --export 5F01BE71 > /var/www/html/repositorio/repo-gpg.key  
```


#### Now position in ```/var/www/html/repositorio```

>
```bash
$ cd /var/www/html/repositorio 
```

#### Execute reprepro -VVV export to create the skeleton the repo

>
```bash
$ sudo reprepro -VVV export
```

#### Create the sysmlinks

>
```bash
$ sudo reprepro -VVV createsymlinks
```

And finnish Now you can add packages


## Add a package

>
```bash
$ reprepro includedeb [DISTRIBUTION] [PACKAGE].deb
```

## Delete a package

>
```bash
$ reprepro remove [DISTRIBUTION] [PACKAGE].deb
```


## Use the repo


Add the file /etc/apt/```sources.list```:

>
```bash
deb http://localhost/repositorio [DISTRIBUTION] [COMPONENTS]
```

or with the IP

>
```bash
deb http://TIP/repositorio [DISTRIBUTION] [COMPONENTS]
```

with domain

>
```bash
deb http://DOMAIN/repositorio [DISTRIBUTION] [COMPONENTS]
```


[SOURCES]

http://huntingbears.com.ve/haciendo-repositorios-de-paquetes-binarios-con-reprepro.html

https://fortu.io/crear-un-repositorio-debian-con-reprepro/