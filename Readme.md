### Container Lifecycle

- docker run = docker create + docker start
  - When you run a Docker container using the docker run command, it's equivalent to executing two separate commands: docker create followed by docker start.

- Create a container : docker create <image-name>
  - This command prepares the container by creating a filesystem snapshot from the specified image.
  
- Start a container: docker start <container-id>
  - Once the container is created, this command executes the startup command defined in the image, initiating the container's main process.

### Exploring hello world image
- docker create hello-world
   - id of the container is generated
   - File system is ready

- docker start <container-id>
  - Starts the container and executes the command.
  - Executed the primary startup command
  - Will just get the id as a output

- docker start -a <container-id>
  - Starts the container and executes the command.
  - Executed the primary startup command
  - ```-a``` : Is going to make the docker actually watch for output from the container and print it out to your terminal.
  - ```-a``` : Kind of attach to the container and watch for output coming from it and print it out at my terminal.
  - The -a flag with docker start allows Docker to attach to the container and display its output in the terminal. Without this flag, Docker doesn't display container output by default.

### Restarting the Container

### Checking Container Status
- Use `docker ps --all` to list all containers, including those that have exited.
- Exited containers remain on the system but are not actively running.

### Creating, Running, and Stopping Containers
1. Start by creating and running a new container using a command like `docker run BusyBox echo hi there`.
2. After execution, check the container status with `docker ps --all`. You'll observe the newly created container listed with its ID and status as "exited".

### Restarting Containers
- Even after a container has exited, it can be restarted.
- To restart a container, use `docker start` followed by the container ID.
- Optionally, add the `-a` flag to see output from the restarted container.

### Understanding Container Lifecycle
- Docker creates a filesystem snapshot for a container when it is created or run.
- The primary command provided during creation or run becomes the default command for the container.
- When a container exits, it can be restarted, executing its default command again.
- Attempting to change the default command upon restarting a container isn't possible; it will execute the original command.
- Solid comprehension of container lifecycle aids in troubleshooting and debugging containerized applications effectively.

### Conclusion
- Understanding the lifecycle of Docker containers is essential for effective management and troubleshooting.
- Mastery of these concepts provides a strong foundation for handling containerized applications in real-world scenarios.


### Importance of Understanding Container Lifecycle
- Proficiency in container lifecycle management facilitates efficient troubleshooting and debugging.
- A comprehensive grasp of these concepts enhances the ability to manage containerized applications effectively.


### Removing the Container

#### Clearing Stopped Containers

1. Begin by checking the status of containers using `docker ps --all`.
2. Stopped containers occupy disk space without serving any active purpose.
3. To delete stopped containers, use the `docker system prune` command.

#### Understanding docker system prune:

- Running `docker system prune` removes stopped containers along with other items like the build cache.
- The build cache consists of images fetched from Docker Hub.
- Deleting the build cache means images will need to be re-downloaded from Docker Hub when required.
- Upon running `docker system prune`, a confirmation prompt appears. Respond with "yes" to proceed.

#### Benefits of docker system prune:

- After execution, the command displays details about the deleted containers and the amount of reclaimed space.
- Following `docker system prune`, check container status again with `docker ps --all` to confirm removal.

#### Recommendations:

- Regularly use `docker system prune` to clean up stopped containers and reclaim disk space.
- Consider running the command after periods of inactivity with Docker or when Docker usage is discontinued.

#### Conclusion:

Efficient management of Docker resources involves regularly removing stopped containers and reclaiming disk space using the `docker system prune` command.
By incorporating this practice into Docker workflows, users can optimize resource utilization and maintain a tidy environment for containerized applications.

## Utilizing Docker Commands for Container Output Management

### Creating and Starting a Container

- We utilized `docker create` followed by a command, such as `BusyBox echo "Hi there"`, which generated a container ID.
- To initiate the container, we used `docker start` followed by the container ID. However, to view the output from the container, we discovered the necessity of appending the `-a` flag.

### Using `docker logs` to Retrieve Container Output

- To streamline the process of accessing container output without relying on the `-a` flag, we employed the `docker logs` command.
- After creating and starting a container, executing `docker logs` followed by the container ID allowed us to retrieve all emitted information.
- Importantly, running `docker logs` does not restart or modify the container; it simply provides a record of the emitted logs.

### Conclusion

- The `docker logs` command serves as a valuable tool for inspecting container output and diagnosing issues without the need for additional flags or container restarts.
- Its utility in debugging and setting up new containers makes it a fundamental component of Docker container management.

By leveraging the `docker logs` command, users can efficiently examine container output and troubleshoot containerized applications with ease.

### Using Redis With Docker

Redis is an in-memory data store commonly used with web applications. Running Redis with Docker offers flexibility and ease of deployment. Below are the steps and details provided for interacting with Redis using both local installation and Docker.


### Using Redis with Docker

Redis is an in-memory data store commonly used with web applications. Running Redis with Docker offers flexibility and ease of deployment. Below are the steps and details provided for interacting with Redis using both local installation and Docker.

### Local Installation:

Install Redis directly on the local machine.
- Start the Redis server by running the command redis-server.
- Open a new terminal window and start the Redis CLI using the command redis-cli.
- Interact with the Redis server using commands such as SET to store data and GET to retrieve data.

### Interacting with Redis Server Using Docker:

#### Start Redis server with Docker using the command:  docker run redis.
- This command pulls the Redis image from Docker Hub and starts a container running the Redis server.
- It may take a moment to download the image if it's not already available locally.
- Warnings during startup are normal, as long as the final line confirms that the server is ready to accept connections.
- Attempting to run Redis CLI directly from another terminal window (redis-cli) will result in an error or "Command not found" message, as the Redis server is running inside the Docker container and not directly accessible from outside.

### Using Docker Exec to Start Redis CLI Inside Container:

In the last section, we started a new instance of the Redis container image, containing a running Redis server. Now, we need to start Redis CLI inside the container. To achieve this, we'll use the Docker exec command.

#### Docker Exec Command Syntax:
docker exec -it <container_id> ``<command>``

- -it: Allows interactive input to the container.
- <container_id>: The ID of the running container.
- <command>: The command to execute inside the container.

### Execute Redis CLI inside the container using Docker exec:
docker exec -it <container_id> redis-cli

### Understanding the -it Flag:
The -it flag plays a crucial role in Docker's interactive mode. It allows the user to interact with the container by providing input from the keyboard, creating an interactive session.

### Understanding the -it Flag in Docker Exec:

In the previous section, we explored the significance of the -it flag when using Docker exec to start Redis CLI inside a Docker container. Let's delve deeper into what this flag does and its importance in the context of Docker container interactions.

### Background on Processes in Linux:

In a Linux environment, each process has three communication channels attached to it: stdin, stdout, and stderr.

- stdin: Used to convey input into the process.
- stdout: Conveys output from the process.
- stderr: Conveys error information from the process.
- Explanation of the -it Flag:

The -it flag in Docker exec is a combination of two separate flags: -i and -t.

- -i: Attaches the terminal to the stdin channel of the new running process inside the container. This ensures that input from the terminal is directed into the process.
- -t: Ensures that the text entered and output displayed is properly formatted for the terminal. While it does more behind the scenes, its main effect is to present text in a readable manner.

### Demonstration Without the -t Flag:

Let's execute Docker exec without the -t flag and observe the differences.

- Obtain the container's ID using docker ps.
- Execute Docker exec with only the -i flag followed by the container ID and redis-cli command.
- Notice that although input can still be provided, the output is not formatted neatly as before.
- Without the -t flag, the terminal lacks the formatting provided by it, resulting in less user-friendly interaction.
- Despite this, commands can still be executed and output retrieved.

### Conclusion:

The -it flag in Docker exec allows for interactive communication with processes inside Docker containers.
By attaching the terminal to the stdin channel (-i) and ensuring proper text formatting (-t), it enables efficient interaction with containerized applications.
Understanding the significance of these flags is essential for effective usage of Docker exec and seamless interaction with Docker containers.

### Opening a Shell Inside a Docker Container Using Docker Exec:

In this section, we'll explore how to gain shell access within a running Docker container using the docker exec command. This capability is essential for debugging and executing commands directly within the container environment.

Execute
```docker exec -it <container_id> sh ```
to open a shell within the container.


- -it: Enables interactive input to the container and ensures proper text formatting.
- <container_id>: Replace with the actual container ID.
- sh: Specifies to start the shell program within the container.

After running the command, you'll be inside the container's shell, denoted by the # prompt.

Within the shell, execute typical Unix commands, such as navigating directories (cd), listing files and directories (ls), executing commands (echo), setting environment variables (export), etc.

### Explanation:

- By using docker exec with the sh command, we open a shell session within the Docker container.
- sh is a command processor or shell program that allows execution of commands within the container environment.
- Similar to how users interact with their local terminal using programs like Bash, Z Shell, Git Bash, or PowerShell, the sh command within the container provides a command prompt for executing commands directly within the container.
- This capability is invaluable for debugging, troubleshooting, and executing commands within the containerized environment.
- The -it flag ensures interactive input and proper text formatting, enhancing the user experience within the container shell.
Conclusion:

- Opening a shell within a Docker container using docker exec -it <container_id> sh provides direct access to the container environment for executing commands and debugging.
- Understanding how to access and utilize the container shell is essential for efficient development and troubleshooting within Docker environments.

### Running a Shell Inside a Docker Container Using docker run:

the previous section, we discussed how to open a shell inside a running container using docker exec. Now, let's explore an alternative approach using docker run to start a container with a shell immediately upon initialization.

#### Procedure:

Open a terminal window to execute Docker commands.

Run the following command:

```docker run -it busybox sh```

- -it: Enables interactive input and attaches to the standard input of the shell.
- busybox: The name of the Docker image to use. Busybox is a lightweight Linux distribution commonly used for testing and debugging.
- sh: Specifies to start the shell program (sh) inside the container.

Upon running the command, a new Docker container is created using the busybox image, and the shell program (sh) is started immediately.

You'll be presented with a shell prompt within the container, where you can execute commands such as ls, ping, echo, etc.

Exit the shell by typing exit or pressing Ctrl+D to return to the host machine's terminal.

Explanation:

- docker run is the command used to start a new Docker container.
- By adding the -it flag along with the image name and the shell command (sh), we instruct Docker to start a container with an interactive shell.
- This approach provides immediate access to a shell inside the container upon initialization, allowing for quick exploration and execution of commands.
- While this method is useful for ad-hoc tasks and debugging, it may not be suitable for long-running services as it replaces the primary command that would typically be executed in the container.
- Common practice involves starting containers with a primary process (e.g., a web server) and then using docker exec to open a shell for debugging purposes.

Conclusion:

- Running a shell inside a Docker container using docker run -it <image_name> sh provides immediate access to a shell for ad-hoc tasks and debugging.
- While useful, this approach replaces the primary command executed by the container and may not be suitable for long-running services.
- Understanding both docker exec and docker run approaches for accessing shells inside Docker containers is essential for effective container management and debugging.

# Docker Basics

## Starting up a Shell Inside a Container

In the previous section, we learned how to start up a shell inside of a container instantly upon its start. If you encounter difficulty exiting the container using `Ctrl + C`, you can alternatively use `Ctrl + D` or type `exit` to exit.

## Understanding Container File System Isolation

It's essential to understand how containers behave with regard to their file systems. Containers do not automatically share their file system with each other. This concept was illustrated with an example where Chrome and NodeJS required different versions of Python and thus operated within their own segmented portions of the hard drive.

To verify this behavior, let's do a quick demo:

1. Open a terminal window and start a new instance of the BusyBox image:

    ```
    docker run -it busybox sh
    ```

2. In another terminal window, start a second container with the same parameters:

    ```
    docker run -it busybox sh
    ```

3. Open a third terminal window and verify the running containers using:

    ```
    docker ps
    ```

4. In the first terminal window, create a new file:

    ```
    touch hi_there
    ```

5. Check the file in the first container:

    ```
    ls
    ```

6. Switch to the second terminal window and check for the file:

    ```
    ls
    ```

You'll notice that the file created in the first container is not visible in the second container. This demonstrates that containers have separate and isolated file systems unless explicitly connected.

In general, unless explicitly connected, containers are considered completely isolated from each other and operate with separate file systems.

## Conclusion

That covers the basics of Docker. In the next section, we'll delve into the next topic. Stay tuned!

