# Docker Tutorial - From 0 to 1

Docker is the company driving the container movement and the only container platform provider to address every application across the hybrid cloud.

## Prerequisites
Docker Account ([Sign up](https://cloud.docker.com/) on Docker).

## Installation
Follow the Docker Documentation to install Docker. This release has been tested on Ubuntu 16.04.

#### Ubuntu

https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/

#### MacOS

https://docs.docker.com/docker-for-mac/install/

#### Windows

https://docs.docker.com/docker-for-windows/install/

## Check Docker and Login

Enter your Username (ID) and Password in the terminal.

```sh
docker login
```

You should see **'Login Succeeded'** if there is no mistake.

## Run Demo App - Upload Image

#### What is Image
Docker Image is the read-only layer which contains the source files and the system environment which supports the source files. To check the current Docker Images, enter

```sh
docker images
```

#### Create Docker Image

Switch to the root of your project directory. In this tutorial, simply swicth to the local repository
```sh
cd <path of the directory>
```

In this tutorial, clone the repository and simply switch to
```sh
cd /Downloads/Docker_Test
```

#### What is Dockerfile

A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using docker build users can create an automated build that executes several command-line instructions in succession.

#### Add Dockerfile in the directory (Already exits in this repository)
```sh
touch Dockerfile
```

#### An example of Dockerfile

```sh

#### Use an official Python runtime as a parent image
FROM python:2.7

#### Set the working directory to /app
WORKDIR /app

#### Copy the current directory contents into the container at /app
ADD . /app

## Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

## Make port 80 available to the world outside this container
EXPOSE 80

## Define environment variable
ENV NAME World

## Run app.py when the container launches
CMD ["python", "app.py"]
```

If you use python, fill **requirements.txt** to satisfy the required environment. **(Already exits in this repository)**

#### Build source files

In this tutorial, Dockerfile and requirements.txt are already been created. So, build the source files to the Image directly.
```sh
docker build -t docker_test .
```

#### Check the new Image
```sh
docker images
```

#### Tag the target Image for pushing
```sh
docker tag docker_test <Docker Account Username>/docker_test
```

#### Push Image
  
Now, there are two Images with same Image ID, push the tagged Image to the Dcoker Hub.
```sh
docker push <Docker Account Username>/Docker_Test
```

## Run Demo App - Download Image

#### Pull Images from the Docker Hub
```sh
docker pull <source_link_On_Docker_Hub>
```
For example

```sh
docker pull hello-world
```

To run the Image, we need to get the Image ID firstly
```sh
docker images
```

In this tutorial, simply run the tagged Image **"Your_Docker_Account_Username/Docker_Test"** that we created just now
```sh
docker run -it <Image_ID> /bin/bash
```

Execute python file
```sh
python hello.py
```
You should see **'Love and Peace' whith any error**.

Exit from the application when you done
```sh
exit
```

## Congratulation!
