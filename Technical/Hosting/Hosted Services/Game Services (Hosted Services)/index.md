The game services are built Docker images, published by a [[Building the Game Services Docker Image|GitHub Action Runner]] on the [GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry).


```yaml
services:
  rabbitmq:
    image: rabbitmq:management
    container_name: rabbitmq
    ports:
      - 15672:15672 # RabbitMQ management plugin
      - 5672:5672 # RabbitMQ message broker
    environment:
      - RABBITMQ_DEFAULT_USER=guest
      - RABBITMQ_DEFAULT_PASS=guest
    volumes:
      - rabbitmq_data:/var/lib/rabbitmq
    networks:
      - app_network
  mongodb:
    image: mongo:latest
    container_name: mongodb
    expose:
      - "27017"
    ports:
      - 27017:27017 # Exposing port 27017 to the host
    volumes:
      - mongodb_data:/data/db
    environment:
      - MONGO_INITDB_DATABASE=${MONGO_INITDB_DATABASE}
      - MONGO_INITDB_ROOT_USERNAME=${MONGO_INITDB_ROOT_USERNAME}
      - MONGO_INITDB_ROOT_PASSWORD=${MONGO_INITDB_ROOT_PASSWORD}
    command:
      - --auth # 👈 This enables authentication
    networks:
      - app_network
  agx.database.server:
    image: ghcr.io/alderoberge/agx.database.server:latest
    build:
      context: .
      dockerfile: AGX.Database.Server/Dockerfile
    expose:
      - "3306"
    ports:
      - 3306:3306 # Exposing port 3306 to the host
    environment:
      - RABBITMQ_HOST=${RABBITMQ_HOST}
      - RABBITMQ_USER=${RABBITMQ_USER}
      - RABBITMQ_PASS=${RABBITMQ_PASS}
      - AGX_SETUP_TYPE=${AGX_SETUP_TYPE}
    networks:
      - app_network
  agx.web.server:
    image: ghcr.io/alderoberge/agx.web.server:latest
    build:
      context: .
      dockerfile: AGX.Web.Server/Dockerfile
    expose:
      - "8443"
    ports:
      - 8443:8443 # Exposing port 8443 to the host
    environment:
      - AGX_SETUP_TYPE=${AGX_SETUP_TYPE}
      - AGX_WEB_SERVER_HOST=${AGX_WEB_SERVER_HOST}
      - AGX_WEB_SERVER_PORT=${AGX_WEB_SERVER_PORT}
      - AGX_WORLD_SERVER_HOST=${AGX_WORLD_SERVER_HOST}
      - AGX_WORLD_SERVER_PORT=${AGX_WORLD_SERVER_PORT}
    networks:
      - app_network
  agx.world.server:
    image: ghcr.io/alderoberge/agx.world.server:latest
    build:
      context: .
      dockerfile: AGX.World.Server/Dockerfile
    expose:
      - "7770"
    ports:
      - 7770:7770 # Exposing port 7770 to the host
    environment:
      - RABBITMQ_HOST=${RABBITMQ_HOST}
      - RABBITMQ_USER=${RABBITMQ_USER}
      - RABBITMQ_PASS=${RABBITMQ_PASS}
      - AGX_SETUP_TYPE=${AGX_SETUP_TYPE}
      - AGX_SERVER_NAME=${AGX_SERVER_NAME}
      - AGX_WEB_SERVER_HOST=${AGX_WEB_SERVER_HOST}
      - AGX_WEB_SERVER_PORT=${AGX_WEB_SERVER_PORT}
      - AGX_WORLD_SERVER_HOST=${AGX_WORLD_SERVER_HOST}
      - AGX_WORLD_SERVER_PORT=${AGX_WORLD_SERVER_PORT}
    networks:
      - app_network
  agx.generation.text:
    image: ghcr.io/alderoberge/agx.generation.text:latest
    build:
      context: .
      dockerfile: AGX.Generation.Text/Dockerfile
    environment:
      - RABBITMQ_HOST=${RABBITMQ_HOST}
      - RABBITMQ_USER=${RABBITMQ_USER}
      - RABBITMQ_PASS=${RABBITMQ_PASS}
    networks:
      - app_network
  playwright:
    image: mcr.microsoft.com/playwright:v1.50.0-noble
    working_dir: /home/pwuser
    user: pwuser
    container_name: playwright
    ports:
      - 3000:3000
    init: true
    tty: true
    stdin_open: true
    environment:
      - DEBUG=pw:* # or use "pw:*" for full logging
    command: /bin/sh -c "npx -y playwright@1.50.0 run-server --port 3000 --host
      playwright"
    networks:
      - app_network
  agx.artisan.browser:
    image: ghcr.io/alderoberge/agx.artisan.browser:latest
    build:
      context: .
      dockerfile: AGX.Artisan.Browser/Dockerfile
    environment:
      - RABBITMQ_HOST=${RABBITMQ_HOST}
      - RABBITMQ_USER=${RABBITMQ_USER}
      - RABBITMQ_PASS=${RABBITMQ_PASS}
      - PLAYWRIGHT_HOST=ws://playwright:3000/
    networks:
      - app_network
  agx.artisan.webapp:
    image: ghcr.io/alderoberge/agx.artisan.webapp:latest
    build:
      context: .
      dockerfile: AGX.Artisan.WebApp/Dockerfile
    expose:
      - "5169"
    ports:
      - 5169:5169 # Exposing port 5169 to the host
    environment:
      - RABBITMQ_HOST=${RABBITMQ_HOST}
      - RABBITMQ_USER=${RABBITMQ_USER}
      - RABBITMQ_PASS=${RABBITMQ_PASS}
      - ASPNETCORE_HTTP_PORTS=5169 # Add this line to ensure the app listens on port 5169
      - ASPNETCORE_URLS=http://+:5169
    networks:
      - app_network
  agx.artisan.server:
    image: ghcr.io/alderoberge/agx.artisan.server:latest
    build:
      context: .
      dockerfile: AGX.Artisan.Server/Dockerfile
    environment:
      - RABBITMQ_HOST=${RABBITMQ_HOST}
      - RABBITMQ_USER=${RABBITMQ_USER}
      - RABBITMQ_PASS=${RABBITMQ_PASS}
    networks:
      - app_network
  agx.discord.server:
    image: ghcr.io/alderoberge/agx.discord.server:latest
    build:
      context: .
      dockerfile: AGX.Discord.Server/Dockerfile
    expose:
      - 8080:8080
    depends_on:
      - rabbitmq
    environment:
      - RABBITMQ_HOST=${RABBITMQ_HOST}
      - RABBITMQ_USER=${RABBITMQ_USER}
      - RABBITMQ_PASS=${RABBITMQ_PASS}
      - AGX_SETUP_TYPE=${AGX_SETUP_TYPE}
      - AGX_SERVER_NAME=${AGX_SERVER_NAME}
      - AGX_WEB_SERVER_HOST=${AGX_WEB_SERVER_HOST}
      - AGX_WEB_SERVER_PORT=${AGX_WEB_SERVER_PORT}
      - AGX_WORLD_SERVER_HOST=${AGX_WORLD_SERVER_HOST}
      - AGX_WORLD_SERVER_PORT=${AGX_WORLD_SERVER_PORT}
    networks:
      - app_network
  agx.analytics:
    image: ghcr.io/alderoberge/agx.analytics:latest
    build:
      context: .
      dockerfile: AGX.Analytics/Dockerfile
    depends_on:
      - rabbitmq
    environment:
      - RABBITMQ_HOST=${RABBITMQ_HOST}
      - RABBITMQ_USER=${RABBITMQ_USER}
      - RABBITMQ_PASS=${RABBITMQ_PASS}
    networks:
      - app_network
volumes:
  rabbitmq_data:
    driver: local
  mongodb_data:
    driver: local
networks:
  app_network:
    driver: bridge

```


Before pulling the containers, you must execute the following command : 

> docker login gchr.io

And provide your GitHub Username and [PAT](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).