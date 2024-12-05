# Tech Cheatsheets

### Docker help
**Docker installation**
- Update package lists (sudo apt update) and install Docker engine (sudo apt install docker.io)
- Add your user to the docker group (sudo usermod -aG docker $USER) so you don't need to use sudo every time
- Verify installation (docker --version)

**Docker image building and container creation**
- Building Docker image and running container for the backend
  - "docker build -t gatech/pokemon -f Dockerfile ./" -> Docker image named gatech/pokemon
  - "docker run --rm -p 8080:8080 -it gatech/pokemon sh"
--
- Make sure your local dependencies match that of the project's dependencies (using npm or yarn)
- Build the Docker image => (DOCKER_BUILDKIT=1 docker build --no-cache -t [image_name] . )
- Create and run a new container (based off the image build) => (docker run -p 3000:3000 -v $(pwd):/app --name [container_name] [image_name] )
- Run the application by going to http://localhost:[port_number]

**Useful commands**
- Start Docker service (sudo systemctl enable docker --now) + check with (sudo systemctl status docker) + stop Docker service with (sudo systemctl stop docker)
- Use (docker ps -a) to see all of the containers you have
- Start or stop with => (docker start <CONTAINER ID> or docker stop <CONTAINER ID> ) => or use the container_name you created earlier
- Remove containers with (docker rm <CONTAINER ID or NAME>
- Check for errors with (docker logs [container_name])
- Make changes within the Docker container itself through its terminal => (docker exec -it pf-container bash)
- Navigate to the project root where the docker-compose.yml file is located, and you can run the command 'docker-compose up -d' | 'docker-compose up --build' for rebuilding and re-running the images
