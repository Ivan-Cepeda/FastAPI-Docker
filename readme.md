Llevar Fast API a Docker y luego hacer deployment.

Lo primero que vamos a hacer es crear un entorno virtual de python. 
``````
python -m venv env
``````
activar el entorno virtual de python
``````
.\env\Scripts\activate
``````
Luego lo ideal instalar en linea de comando Fast API
``````
pip install fastapi uvicorn
``````
crear una carpeta en la misma jerarquía, que la del entorno virtual de python. En este caso la llame "app"
``````
mkdir app
``````
Ingresar a la carpeta creada
``````
cd app
``````

