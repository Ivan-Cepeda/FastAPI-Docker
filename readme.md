Llevar Fast API a Docker y luego hacer deployment.

Lo primero que vamos a hacer es crear un entorno virtual de python. 
``````
python -m venv env
``````
Activar el entorno virtual de python
``````
.\env\Scripts\activate
``````
Luego lo ideal instalar en linea de comando Fast API
``````
pip install fastapi uvicorn
``````
Crear una carpeta en la misma jerarquía, que la del entorno virtual de python. En este caso la llame "app"
``````
mkdir app
``````
Ingresar a la carpeta creada
``````
cd app
``````
Crear los archivos main.py y __init__.py, tus módulos, agrega los archivos de tu app.

Al finalizar tu application e instalar las dependencias, se debe guardar todos los módulos y versiones usadas en un archivo requirements.txt
``````
pip freeze > requirements.txt
``````
luego crea el archivo Dockerfile aquí un ejemplo basado en la documentación de FastAPI
``````
FROM python:3.9

WORKDIR /code

COPY ./requirements.txt /code/requirements.txt

RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

COPY ./app /code/app

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
``````
Luego asegurate de tener corriendo docker para construir la imagen de tu aplicación.
``````
docker build -t myapp .
``````
Demora un poco en crearse la imagen.

En este punto asegúrate de tener una cuenta en [Dockerhub](https://hub.docker.com/)
con los datos de tu cuenta te toca inciar sesión desde la línea de comando usando. 
``````
docker login
``````
Luego de ingresar debes indicar el nombre de tu imagen asociado a tu usuario.
``````
docker tag myapp usuario/myapp
``````
El siguiente paso será cargar la imagen a tu repo de docker hub.
``````
docker push timcepeda/myapp
``````
Finalizado este paso es momento de ir a [render](https://render.com/) para deployar tu imagen de forma rápida. 

- Crea una cuenta en render
- Le das en crear un nuevo servicio web, en este caso usamos la versión free. 
- Indicas que es desde una imagen existente
- agrega la ruta de tu imagen como pista, sería usuario/myapp:latest
- Espera mientras se realiza el deployment

Al finalizar te pasará la url desde dónde puedes acceder a tu API.

