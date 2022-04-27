# VIDEO / COURSE / REFERENCE

- [https://app.pluralsight.com/course-player?courseId=37092a4b-64af-429f-ac0e-c30ace526653](https://app.pluralsight.com/course-player?courseId=37092a4b-64af-429f-ac0e-c30ace526653)
- [https://app.pluralsight.com/library/courses/docker-web-development/table-of-contents](https://app.pluralsight.com/library/courses/docker-web-development/table-of-contents)
- [https://dev.to/dhravya/docker-explained-to-a-5-year-old-2cbg](https://dev.to/dhravya/docker-explained-to-a-5-year-old-2cbg)
- https://github.com/bobbyiliev/introduction-to-docker-ebook

# CONCEPTS

### WHAT IS DOCKER

- is a way to *containerize* applications (putting code in boxes that can work on their own).

### CONTAINERS

- virtual operating system (with its own folders, files, etc...)
- They use `images`

### CONTAINERIZATION

- Trap a Bee on its own honeycomb so it can live forever

### IMAGES

- Is a set of instructions for creating a container.
- It uses `Dockerfile`

### IMAGES vs CONTAINERS

- image = `class Computer` (stopped `container`) = read/only
- container = `new Computer()` (running `image`) = read/writer

### CONTAINER REGISTRY

- docker's `npm`
- where we store `images` so we can reuse it for later

### CONTAINERIZED APP

- app that runs inside a container
- similar to a lightweight virtual machine

### DOCKERFILE

- text document that contains all the commands on the CLI to assemble an image.

### DOCKER COMPOSE

- multi-container orchestration mechanism
- manages the whole application lifecycle
- way to avoid multiple docker commands
- a set of SIMPLE instructions
- describes the desired state in a declarative way (manifest)
- it is all about `services`
- it expects a `docker-compose.yml` file

### DOCKER COMPOSE WORKFLOW

```jsx
BUILD            // what folder, what service...
ENVIRONMENT      // env variables...
IMAGE            // use images
NETWORKS         // associate a service with a network...
PORTS            // define ports
VOLUMES          // define volumes
```

### DOCKER COMPOSE COMMANDS

```jsx
docker-compose build.  // trigger the build of everything defined in the .yml
docker-compose up.     // create and start the container (similar to docker run)
docker-compose down.   // stop and remove the containers
docker-compose logs
docker-compose ps
docker-compose stop
docker-compose start
```

### DOCKER SWARM

- container orchestration
- allows you to have multiple docker containers running at the same time
- unlocks docker services

> how can you make docker works across multiple node sharing containers?
> 
### MULTI CONTAINER COMMUNICATION

- BRIDGE NETWORK
    - make usage of the `... --net`
    - custom isolated bridge network
    - group of containers that each one can access each ohter
    - a little more elegant
    
    ```jsx
    // Creating a network
    docker network create --drive bridge NAME_OF_ISOLATED_NETWORK
    
    // Linking a container to a network
    docker run -d --net=NAME_OF_ISOLATED_NETWORK CONTAINER_NAME
    ```
    
- LEGACY LINKING
    - make usage of the `... --link`
    - it creates a bridge network based on each container's name
    - **give a container a name and then another container can link to it using the same name**
    - a simple technique
    
    ```jsx
    docker run -d --name NAME_POSTGRES postgres
    
    docker run -d -p 5000:5000 --link NAME_POSTGRES:NAME_INTERNAL_ALIAS ANOTHER_CONTAINER_NAME_THAT_WILL_BE_LINKED
    ```
    

# COMMANDS / MANIFESTS

### DOCKERFILE - FLOW

```jsx
FROM                // gives the ground, after that, when running it uses the Host's Kernel
METADATA            // sets the name, title, label, etc
COPY                // copy the content to a specific folder
WORKDIR             // set to where docker needs to look at
RUN                 // install the dependencies
ENTRYPOINT          // sets the command that starts the app
EXPOSE              // expose that the container will be running internally
```

### BUILDING AN IMAGE

```jsx
// When you want to set/build/getready all the container
docker image build -t <hubname>/<repo>:<version> .
```

### PUSHING TO THE DOCKER HUB

```jsx
// When you want to share to the Docker Hub (npm)
docker image push <hubname>/<repo>:<version>
```

### REMOVING A LOCAL IMAGE

```jsx
// When you want to remove a local image
docker image rm <imageName>

docker rmi <imageName>
```

### RUNNING/CREATING A CONTAINER from a sourceode

```jsx
// Run is a combination of create and start. 
// It creates the container and starts it.

// Example 01
docker container run -d --name <NAME> -p <PORT-TO:PORT-FROM> <DOCKERHUBFROM>

docker container run 
-d                  // detached from the current terminal
--name web          // giving the container a name web
-p 8000:8080        // mapping everything from 8080 to 8000
luisvalgoi/gsd:01   // pulling from the hub

// Example 02
docker run -p 8080:3000 -v $(pwd):/var/www -w "/var/www"

docker run
-p 8080:3000        // mapping everything from 3000 to 8080
-v $(pwd):/var/www  // sets a volume that points to the current dir with the volume name as /var/www
-w "/var/www"       // uses the /var/www as the working directory  
```

### INSPECTING A CONTAINER

```jsx
// When you want to know where it is located for instance...
docker inspect <name>
```

### STOPPING A CONTAINER

```jsx
// When you want to stop a running container
docker container stop <name>
```

### STARTING A CONTAINER

```jsx
// When you want to only run a stopped container
docker container start <name>
```

### REMOVING A CONTAINER

```jsx
// When you want to remove a container
docker container rm <name> 
```

### RUNNING A COMMAND INSIDE THE CONTAINER

```jsx
// When you want to run some command inside the container
docker exec <id> <command....>
docker exec h1hguiid1j node app.js
```

### LISTING

```jsx
docker image ls -a     // show all the images
docker image ls        // show the 'active' images

docker network ls      // show all the networks

docker container ls -a // show all the containers
docker container ls    // show the 'active' containers

docker ps ls -a        // show all the containers
docker ps la           // show the 'active' containers
```
