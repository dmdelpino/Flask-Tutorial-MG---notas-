# Flask-Tutorial-MG---notas-
Apuntes del microblog en https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world


# CAPITULO 1 - Introducción

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
from app import app_clase  ====> importa la instancia de la clase Flask "app_clase" desde el paquete "app"
```

---

### d. Prueba de la aplicación

> $ export FLASK_APP=microblog.py
> $ flask run

Luego se ingresa a la dirección local en http://127.0.0.1 o http://localhost:5000 

Para evitar tener que realizar esta operación cada vez que se desea correr el servidor se puede instalar el paquete
*python-dotenv*. Una vez instalado se escribe la variable de ambiente en un archivo con extensión .flaskenv

> /microblog/.flaskenv
```
FLASK_APP=microblog.py
```

---
---

# CAPITULO 2 - Templates (plantillas)

### a. Que es una plantilla

Permite diferenciar la lógica de funcionamiento de la aplicación del diseño de la web visible al usuario. Se guardan en
un directorio especialmente dedicado ("templates").

> /microblog/app/templates/index.html   ====> plantilla de la página principal

```
<html>
    <head>
        <title>{{ title }} - Microblog</title>      ====> Elemento dinámico entre {{ y }}. Variable, solo se define su 
    </head>                                               valor al momento de ejecución.
    <body>
        <h1>Hello, {{ user.username }}!</h1>        ====> Igual anterior.
    </body>
</html>
```

Luego se actualiza el archivo __routes.py__ para agregar la información que va a ser mostrada mediante la plantilla creada.

> /microblog/app/routes.py      ====> usar la función render\_template()

```
from flask import render_template       
from app import app_clase

@app.route('/')
@app.route('/index')
def index():
    user_nombre = {'username': 'Miguel'}        ====> diccionario que guarda los datos de usuario, provisoriamente.
    return render_template('index.html', title='Home', user=user_nombre)   
```

La función render\_template() importada de flask transforma la plantilla __index.html__ creada previamente en una página 
web completa. Los argumentos que se le pasan reemplazan a los elementos dinámicos previamente agregados en esa página.
* Todos los bloques __{{ ... }}__ son reemplazados por los valores indicados en los argumentos de la función.

----

### b. Declaraciones condicionales

Los bloques __{% ... %}__ permiten establecer estructuras de control. Se modifica __index.html__ para incorporar una de ellas.

> /microblog/app/templates/index.html

```
<html>
    <head>
        {% if title %}
        <title>{{ title }} - Microblog</title>
        {% else %}
        <title>Welcome to Microblog!</title>
        {% endif %}
    </head>
    <body>
        <h1>Hello, {{ user.username }}!</h1>
    </body>
</html>
```

La estructura condicional coloca el título definido en la función render\_template(), llamada por index() en el archivo
routes.py, para la URL "index". Si no se le pasa ningún __title__ entonces utiliza el genérico indicado en __else__.

---

### Bucles ('loops')

