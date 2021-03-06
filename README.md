# hello-docker
A sample helloworld to try docker.

## Build
- Create docker images for each of the projects :
```
	$ cd helloworld
	$ docker build -t helloworld:v1 .
	$ cd ../loadbalancerhw
	$ docker build -t hwloadbalancer:v1 .
```

## Run
- Start two instances with a shared volume for the visits counter :
```
	$ docker run -d --volume /tmp/hello --name helloworld1 helloworld:v1
	$ docker run -d --volumes-from helloworld1 --name helloworld2 helloworld:v1
```
- Start the loadbalancer listenning on port 80 :
```
	$ docker run -d -p 80:80 --link helloworld1:hw1 --link helloworld2:hw2 hwloadbalancer:v1
```
- Now you can reach your app in normal or debug mode with :
```
	http://localhost/greetings
	http://localhost/greetings?debug=1
```

## Notes
- According to your system setup you may need to be root to execute previous commands.
