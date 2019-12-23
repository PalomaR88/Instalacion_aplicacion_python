# Instalación de aplicación python

En esta tarea vamos a desplegar un CMS python . Hemos elegido Mezzanine, pero puedes elegir otro CMS python basado en django.

## Instala el CMS en el entorno de desarrollo. Debes utilizar un entorno virtual.

### Creación del entorno virutal
Se crea un entorno virtual:
~~~
paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine$ python3 -m venv mezzanine
paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine$ source mezzanine/bin/activate
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine$  
~~~

A continuación se instala mezzanine:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine$ pip install mezzanine
~~~

Se crea el fichero requetiments que contrendrá los paquetes:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine$ pip freeze > requirements.txt
~~~

> Quizás antes hay que actualizar pip:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine$ pip install --upgrade pip
~~~

De esta forma, el contenido de requeriment.txt es:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine$ cat requirements.txt 
beautifulsoup4==4.8.1
bleach==3.1.0
certifi==2019.11.28
chardet==3.0.4
Django==1.11.27
django-contrib-comments==1.9.2
filebrowser-safe==0.5.0
future==0.18.2
grappelli-safe==0.5.2
idna==2.8
Mezzanine==4.3.1
oauthlib==3.1.0
Pillow==6.2.1
pkg-resources==0.0.0
pytz==2019.3
requests==2.22.0
requests-oauthlib==1.3.0
six==1.13.0
soupsieve==1.9.5
tzlocal==2.0.0
urllib3==1.25.7
webencodings==0.5.1
~~~

> Es posible que en requeriment.txt aparezca la línea "pkg-resources==0.0.0" en cuyo caso hay que eliminarla para evitar conflictos.

### Proyecto mezzanine
Para crear el proyecto:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine$ mezzanine-project pythoncms
~~~

Y la base de datos:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine$ python3 pythoncms/manage.py migrate
~~~

Se crear el superuser:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine$ python3 pythoncms/manage.py createsuperuser
Username (leave blank to use 'paloma'): 
Email address: palomagarciacampon08@gmail.com
Password: 
Password (again): 
Superuser created successfully.
~~~

Y se abre el servidor:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine$ python3 pythoncms/manage.py runserver
              .....
          _d^^^^^^^^^b_
       .d''           ``b.
     .p'                `q.
    .d'                   `b.
   .d'                     `b.   * Mezzanine 4.3.1
   ::                       ::   * Django 1.11.27
  ::    M E Z Z A N I N E    ::  * Python 3.7.3
   ::                       ::   * SQLite 3.27.2
   `p.                     .q'   * Linux 4.19.0-6-amd64
    `p.                   .q'
     `b.                 .d'
       `q..          ..p'
          ^q........p^
              ''''

Performing system checks...

System check identified no issues (0 silenced).
December 20, 2019 - 11:43:02
Django version 1.11.27, using settings 'pythoncms.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
~~~

![run mezzanine](images/aimg.ong)


## Personaliza la página (cambia el nombre al blog y pon tu nombre) y añade contenido (algún artículo con alguna imagen).

Desde la página de administrador se modifica el nombre de la página en el apartado settings.

![cambio de nombre](images/bimg.ong)

Y se crea algún blog:

![cambio de nombre](images/cimg.ong)
![cambio de nombre](images/dimg.ong)


## Guarda los ficheros generados durante la instalación en un repositorio github. Guarda también en ese repositorio la copia de seguridad de la bese de datos.

Se guardan los fichero:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine/pythoncms$ python3 manage.py dumpdata > db.json
~~~

Y se sube todo a un repositorio de GitHub.
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine/pythoncms$ git init
Inicializado repositorio Git vacío en /home/paloma/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine/pythoncms/.git/
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine/pythoncms$ git add *
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine/pythoncms$ git commit -m 'subir contenido'
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine/pythoncms$ git remote add origin git@github.com:PalomaR88/mezzanine.git
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/Maquinas-claud/mezzanine/mezzanine/pythoncms$ git push -u origin master
~~~


## Realiza el despliegue de la aplicación en tu entorno de producción (servidor web y servidor de base de datos en el cloud). Utiliza un entorno virtual. Como servidor de aplicación puedes usar gunicorn o uwsgi (crea una unidad systemd para gestionar este servicio). La aplicación será accesible en la url python.tunombre.gonzalonazareno.org.

Se clona el repositorio:
~~~
[centos@salmorejo ~]$ git clone https://github.com/PalomaR88/mezzanine
~~~

Se instala python:
~~~
[centos@salmorejo ~]$ sudo dnf install python36 python36-devel
~~~

Se crea un entornio virtual:
~~~
[centos@salmorejo ~]$ python3.6 -m venv entorno
[centos@salmorejo ~]$ source entorno/bin/activate
(entorno) [centos@salmorejo ~]$ 
(entorno) [centos@salmorejo mezzanine]$ pip install -r requirements.txt
~~~

Se crea la base de datos:
~~~
MariaDB [(none)]> create database pythoncms;
Query OK, 1 row affected (0.05 sec)

MariaDB [(none)]> create user python identified by 'python';
Query OK, 0 rows affected (0.08 sec)

MariaDB [(none)]> grant all privileges on pythoncms.* to python;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> flush privileges;
Query OK, 0 rows affected (0.04 sec)
~~~

~~~
DATABASES = {
    'default': {
          'ENGINE': 'mysql.connector.django',
          'NAME': 'pythoncms',
          'USER': 'python',
          'PASSWORD': 'python',
          'HOST': 'sql.paloma.gonzalonazareno.org',
          'PORT': '',
    }
}
~~~
~~~
ALLOWED_HOSTS = ['python.paloma.gonzalonazareno.org']
~~~

~~~
(entorno) [centos@salmorejo pythoncms]$ pip install mysql-connector-python
Collecting mysql-connector-python
~~~
~~~
(entorno) [centos@salmorejo pythoncms]$ python3 manage.py migrate
~~~
