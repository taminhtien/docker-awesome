# How to run a Rails app on Docker's Rails image

## 1. Dockerize

Create Dockerfile in your project:

```
$ cd ~/Workspace/practices/rails/devise-in-depth
$ touch Dockerfile
```

Due to ```Rails:onbuild``` encounters SSL error when installing gems, we will use ```Rails:latest``` to build our image.

*Note #1:* To fix the SSL error when installing gems, we can change ```https``` to ```http``` as a temporary method.

```
source 'https://rubygems.org'
source 'http://rubygems.org'
```

> Example Dockfile: https://www.packet.net/blog/how-to-run-your-rails-app-on-docker/

```
FROM rails:latest

ENV HOME /home/rails/webapp

# Install PGsql dependencies and js engine

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

WORKDIR $HOME

# Install gems

ADD Gemfile* $HOME/

RUN bundle install

# Add the app code

ADD . $HOME

# Default command

CMD ["rails", "server", "--binding", "0.0.0.0”]
```

*Note #2:* The last line in Dockerfile seemingly binds 0.0.0.0 to rails server.

## 2. Build images

```
$ docker build -t image-name .

image-name: the name of image you want to create
dot(.): Remember that not to omit the dot (.) at the end of this command, it will mount current directory (your project) to created image file
```

In our case:

```
$ docker build -t devise-in-depth .
```

## 3. Run created image

```
$ docker run -d -p 3000:3000 image-name

The '-d' flag tells docker daemon to run this container in 'daemon mode'
THe '-p' flag tells docker to let us choose a port binding between the host and the container
```

In our case:

```
$ docker run -d -p 3000:3000 devise-in-depth
```

You can try:

```
% docker run -d -p 3000:3000 devise-in-depth /bin/bash
```

to access to the container and run ```rails s``` to start server.

## 4. Test on browser

Because the ```localhost:3000``` does not run in my case. I will find what IP address of the running container is.

```
$ docker inspect ImageID | grep IPAddress
Ex: docker inspect ffba65d0e354 | grep IPAddress
```