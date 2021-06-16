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

---

### c. Creación de un paquete
Paquete: subdirectorio que tiene un archivo *\_\_init_\_\.py*

Se lo puede importar.

>/microblog/app/\_\_init\_\_.py: instancia de la aplicación Flask

```
from flask import Flask           ====> importa la clase "Flask" del paquete flask
app_clase = Flask(__name__)       ====> crea la instancia de la clase Flask con el nombre "app_clase".
from app import routes            ====> desde el módulo "app" importa routes.py
```

>/microblog/app/routes.py: indica las URL que la aplicación va a implementar. Cada manejador de la lógica se programa 
> como función de Python (view function). Cada función está asociada a una o mas URL, para que Flask sepa como reaccionar
> de acuerdo a la URL ingresada
 
```
from app import app_clase

@app.route('/')             ====> @app.route es un decorador. Asocia la función index() a las URL que se le pasa a los  
@app.route('/index')              decoradores como variable. Tanto la URL "/" como "index" van a llamar a la función index(). El valor   
def index():                      devuelto por esa función se le devuelve al browser.  
    return "Hello, World!" 
```

>/microblog/microblog.py
 
```
from app import app_clase  ====> importa la instancia de la clase Flask "app" desde el paquete también llamado "app"
```
