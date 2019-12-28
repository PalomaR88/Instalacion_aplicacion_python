# Instalación de aplicación python

En esta tarea vamos a desplegar un CMS python. Hemos elegido Mezzanine, pero puedes elegir otro CMS python basado en django.

## Instala el CMS en el entorno de desarrollo. Debes utilizar un entorno virtual.

### Creación del entorno virutal
Se crea un entorno virtual:
~~~
paloma@coatlicue:~/DISCO2/CICLO II$ python3 -m venv mezzanine
paloma@coatlicue:~/DISCO2/CICLO II$ source mezzanine/bin/activate
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II$  
~~~

A continuación se instala mezzanine:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine$ pip install mezzanine
~~~




Se crea el fichero requetiments que contrendrá los paquetes:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine$ pip freeze > requirements.txt
~~~

> Quizás antes hay que actualizar pip:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine$ pip install --upgrade pip
~~~

De esta forma, el contenido de requeriment.txt es:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine$ cat requirements.txt 
beautifulsoup4==4.8.2
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
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine$ mezzanine-project python_iaw
~~~

Y la base de datos:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine$ python3 python_iaw/manage.py migrate
~~~

Se crear el superuser:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine$ python3 python_iaw/manage.py createsuperuser
Username (leave blank to use 'paloma'): 
Email address: palomagarciacampon08@gmail.com
Password: 
Password (again): 
Superuser created successfully.
~~~

Y se abre el servidor:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine$ python3 python_iaw/manage.py runserver
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
December 27, 2019 - 20:08:05
Django version 1.11.27, using settings 'python_iaw.settings'
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

Se realiza una copia de la base de datos en un fichero .json:
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine$ python3 python_iaw/manage.py dumpdata > python_iaw/CopiaBD.json
~~~

Y se sube todo a un repositorio de GitHub.
~~~
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine/python_iaw$ git init
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine/python_iaw$ git add -f *
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine/python_iaw$ git commit -m "Subir fichero aplicaciones cms python"
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine/python_iaw$ git remote add origin git@github.com:PalomaR88/python_iaw.git
(mezzanine) paloma@coatlicue:~/DISCO2/CICLO II/mezzanine/python_iaw$ git push -u origin master
~~~


## Realiza el despliegue de la aplicación en tu entorno de producción (servidor web y servidor de base de datos en el cloud). Utiliza un entorno virtual. Como servidor de aplicación puedes usar gunicorn o uwsgi (crea una unidad systemd para gestionar este servicio). La aplicación será accesible en la url python.tunombre.gonzalonazareno.org.

Se clona el repositorio:
~~~
[centos@salmorejo ~]$ git clone https://github.com/PalomaR88/python_iaw.git
~~~

Se instala python:
~~~
[centos@salmorejo ~]$ sudo dnf install python36 python36-devel
~~~

Se crea el entorno virtual:
~~~
[centos@salmorejo ~]$ python3.6 -m venv entorno
[centos@salmorejo ~]$ source entorno/bin/activate
(entorno) [centos@salmorejo ~]$ 
~~~

Se instala todos los paquetes que aparecen en requirement.txt:
~~~
(entorno) [centos@salmorejo python_iaw]$ pip install -r requirements.txt
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

En el fichero settings.py se modifican los siguientes valores:
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

Se instala el paquete necesario para que python se conecte a mysql:
~~~
(entorno) [centos@salmorejo python_iaw]$ pip install mysql-connector-python
~~~

Y se comienza la migración:
~~~
(entorno) [centos@salmorejo pythoncms]$ python3 manage.py migrate
(entorno) [centos@salmorejo python_iaw]$ python3 manage.py loaddata CopiaBD.json 