# Explanation of Dockerfile Commands

- `FROM python:3.9-slim`  
  Specifies the base image for your container. Here, it uses a lightweight Python 3.9 image from Docker Hub.

- `WORKDIR /app`  
  Sets the working directory inside the container to `/app`. All following commands will be run in this directory.

- `COPY . /app`  
  Copies all files and folders from your current directory on the host machine into the `/app` directory in the container.

- `RUN pip install --no-cache-dir -r requirements.txt`  
  Runs a command inside the container to install Python dependencies listed in `requirements.txt`. `--no-cache-dir` keeps the image size smaller by not caching packages.

- `EXPOSE 80`  
  Documents that the container listens on port 80 at runtime. This doesn’t publish the port but informs Docker and users.

- `ENV NAME World`  
  Sets an environment variable named `NAME` with the value `World` inside the container.

- `CMD ["python", "app.py"]`  
  Specifies the default command to run when the container starts — here, it runs the Python script `app.py`.
