Writing simple flask app

1. create folder for your project for example ``project``. Inside this folder create 2 file.  
   1- ``app.py`` 2- ``Dockerfile``
2. copy this code inside ``app.py`` file:
    ```
    import os
    from flask import Flask

    app = Flask(__name__)

    group_number = os.environ.get('GROUP_NUMBER')
        
    @app.route("/")
    def hello_world():
        return f'Hello World!Group {group_number}'

    if __name__ == "__main__":
        app.run(host='0.0.0.0', port=5005)

   ``` 
3. copy this code inside ``Dockerfile`` file
    ```
     FROM python:3.10-slim-buster

     RUN pip install flask
     
     WORKDIR /my_app
     
     EXPOSE 5005
     
     COPY . .
     
     CMD ["python3","app.py"]
   ```
4. open your cmd where you created folder ``project``. and paste this commands 
    ```
    docker build -t {image_name}:v1 .
   ```
   if you see all images you can see new image which you created. Then you should run container using this image
    ```
   docker run -d -p {port_number}:5005 -e GROUP_NUMBER=5555 
   {image_name}:v1
   ```
   If everything is ok, open your browser and enter ``http:localhost:{port_number}``
    
    ![img.png](img.png)
   
