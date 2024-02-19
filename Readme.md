### docker run
- The docker run command is used to create and run a container from a Docker image.
- Syntax: ```docker run [OPTIONS] IMAGE_NAME [COMMAND] [ARG...]```
- Running docker run hello-world likely involved Docker retrieving the specified image (e.g., hello-world) from the local cache or Docker Hub
-  docker run command is the entry point for creating and running Docker containers, providing a simple yet powerful mechanism for deploying applications in isolated environments


### Overriding Default Commands (docker run imagename)
- When using Docker, each container is created based on a specific image. These images contain a filesystem snapshot along with a default startup command. Typically, when you execute docker run imagename, Docker creates a new container from the specified image and automatically executes the default startup command within the container.

#### Let's elaborate on this process with an example:

- Suppose we have an image named myapp that contains a simple web server. 
- The default startup command in this image is to start the web server and listen on port 80.
- If we run the following command: ```docker run myapp```
  - Docker will create a new container using the myapp image and automatically start the web server inside the container. 
  - As a result, the web server will begin listening on port 80, and we can access it using a web browser or other HTTP clients.
  - However, sometimes we may want to override the default startup command and execute a different command within the container. 
  - This could be useful for debugging purposes, running additional setup tasks, or performing custom actions.

- To override the default command, we can specify the desired command after the image name when using the docker run command. For example:
- ```docker run myapp ls -l```
  - In this command, we're instructing Docker to create a new container from the myapp image and execute the ls -l command inside the container. 
  - Instead of starting the web server, the container will now execute the ls -l command, which lists the contents of the current directory in long format.

  

**More on Docker Run:**
- Exploring variations of the `docker run` command, focusing on overriding the default startup command of Docker containers.

**Basic Syntax:**
- `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`: Runs a command in a new container based on the specified image.
- The default command provided in the image is executed unless overridden.

**Override Default Command:**
- To override the default command, specify an alternate command after the image name.
- Example: `docker run IMAGE COMMAND [ARG...]`.
- The specified command will be executed inside the container instead of the default command.

**Example 1: Echo Command Override:**
- Execute `docker run busybox echo "hi there"` to print "hi there" inside the container.
- Demonstrates overriding the default command with the `echo` command.
- Subsequent variations can change the text printed by `echo`.

**Example 2: ls Command Override:**
- Execute `docker run busybox ls` to list files and folders inside the container.
- Shows how to use the `ls` command to view the container's filesystem.
- The listed directories (`bin`, `dev`, `home`, etc.) belong to the container, not the host system.

**Using Busybox Image:**
- Busybox image contains essential Unix utilities like `ls` and `echo`.
- Suitable for demonstrating command overrides due to its rich set of commands.

**Comparison with hello-world Image:**
- Attempting to use `ls` or `echo` with the `hello-world` image results in errors.
- `hello-world` image contains only a single program to print a greeting message.
- Demonstrates that command overrides depend on the programs available in the container's filesystem.

**Conclusion:**
- Variations of the `docker run` command allow overriding the default command executed in Docker containers.
- Understanding the content of the image's filesystem is crucial for selecting appropriate override commands.
- Busybox image provides a versatile environment for experimenting with different commands.

**Note:**
- The success of command overrides depends on the availability of the specified command within the container's filesystem.
- Choose images with suitable utilities based on the desired override commands.

## Managing Docker Containers with `docker ps`

The `docker ps` command is a fundamental tool in managing Docker containers. It allows us to view the status of containers running on our machine. Let's explore how it works and its common use cases.

### Viewing Running Containers

When you run `docker ps` in your terminal, it lists all the currently running containers. If no containers are running, it will display a message indicating that there are no containers.

### Common Use Cases:
- Monitoring Running Containers: Docker PS provides real-time information about running containers, allowing users to monitor their status and resource usage.
- Identifying Container IDs: The Container ID column provides unique identifiers for each container, which is useful for performing actions on specific containers, such as stopping or restarting them.

### Containers with Short Lifespans
- Sometimes, containers are started, run a command, and then stop immediately. These containers do not appear in the output of docker ps because they have already exited by the time the command is executed.
- Example: Running a Container with Short Lifespan: docker run busybox echo "Hello, World!"

### Observations:

- In this example, the container runs the echo command to print "Hello, World!" and then exits immediately.
- When you run docker ps, you won't see this container listed because it has already stopped.

### Viewing All Containers
- docker ps --all
- To view all containers, including those that have exited, you can use the docker ps command with the --all or -a flag.
- This command displays a list of all containers, including both running and exited containers.
- Exited containers are marked with a status indicating their stopped state.

### Command in a glance 

- docker run hello-world
- docker run busybox
- docker run busybox ls
- docker run busybox echo "hi there"
- docker run busybox ping google.com
- docker ps
- docker ps --all