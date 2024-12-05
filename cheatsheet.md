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


---

### Git help
- New remotes => "git remote -v" | "git remote add [remote-name] [repo-url]"
- git fetch allows you to reset your local branch to match the remote branch 
  - 'git fetch origin' | 'git reset --hard origin/<branch_name>'
- New git branch: 'git checkout -b <new_branch_name>"

---

### React help
**Layered/MVC architecture intuition**
- Database-Entity-Repository-Service-DTO-Controller-UI => the two-flow of data
- Entities are entirely for the data layer, representing the structure of the data and how it's stored in the database (assisted by JPA so SQL isn't necessary)
- Repositories are also entirely for the data layer, providing the interface for CRUD operations on the data represented by the entities
- Services are the core of the backend logic layer and use repositories to interact with the data layer
- DTOs play a key role in the backend logic layer, encapsulating data and transferring it between services and controllers | they also represent the data that's used in the UI | DTOs bridge data exchange between the UI and the backend

**React UI Intuition**
- The React UI (frontend) is built with components | The UI handles user input through dropdown menus and buttons | The UI displays data fetched from the backend and updates dynamically based on backend responses
- The UI "communicates" with the backend through API requests (REST controllers) | these requests trigger the "services" (the core application logic), and these services work with repositories that directly interact with the database to fetch or persist data
- The "connection" -> The React UI makes API calls to the Spring Boot backend | the backend sends data (JSON responses) to the UI, and the UI sends commands or actions to the backend | the UI uses React's state management features to update the display based on the data received from the backend
- Example "flow" -> User selects Pokemon in the BattleView dropdown menus | User clicks the "Start Battle" button | UI sends a request to the corresponding endpoint (like "/battle/start") with the selected Pokemon | The backend's BattleService simulates the battle and sends updates to the UI (like battle logs, Pokemon HP changes) | The UI updates the display dynamically based on these updates

---

### Java help
**Debugging**
- Take advantage of error logging and stack tracing to pinpoint the source of bugs
  - Use try-catch blocks, and for catch use "Catch (Exception e) { System.err.println(" " + e.getMessage()); e.printStackTrace(); throw e; }
