# Flask-Tutorial-MG---notas-
Apuntes del microblog en https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world


# CAPITULO 1

### a. Creación de virtual environments
A efectos de mantener la versión con la que se comenzó a trabajar, conviene utilizar el ambiente virtual:

`$ python3 -m venv nombre_ambiente_virtual`

(dentro del directorio raiz de la aplicación)

---

### b. Activar virtual environment

`$ source venv/bin/activate`

### c. Creación de un paquete </h3>
Paquete: subdirectorio que tiene un archivo *\_\_init_\_\.py*

Se lo puede importar.

>microblog/app/\_\_init\_\_.py: instancia de la aplicación Flask

```
from flask import Flask
app = Flask(__name__)
from app import routes
```
