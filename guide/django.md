Writing dockerfile for django project
1. create folder for your new project ``django-docker``
2. open this folder from your terminal(cmd)
3. run this command
    ```
    python3 -m venv venv
   ```
   for linux,mac:
   ```
    source venv/bin/activate
   ```
   for windows:
   ```
    source venv/Scripts/activate
   ```
   ```
    pip3 install django
    pip3 freeze > requirements.txt
    django-admin startproject config .
   ```
4. If you want to run this django project your local computer, run this command
    ``` 
   python3 manage.py runserver
   ```
   ![img.png](img.png)
5. Let`s start writing ``Dockerfile``
   ```
   FROM python:3.11-slim-buster

   WORKDIR /django_docker
   
   COPY . .
   
   RUN pip3 install -r requirements.txt
   
   EXPOSE 8000
   
   CMD ["python3","manage.py","runserver","0.0.0.0:8000"]
   ```
6. So, now we should create docke image and container from Dockerfile. 
   creating image:
   ```
      docker build -t {image-name}:v1 .
   ```
   creating container:
   ```
   docker run -d -p {port_number}:8000 
   {image_name}:v1
   ```
7. If you open browser and enter ``http://localhost:{port_number}``, you can see rocket