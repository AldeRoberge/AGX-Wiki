To publish your content or layout and style changes, we use a combination of Docker images and Dockge, a fancy pants *docker-compose.yml* editor, so we can easily update the generated website.


We use git-sync to automatically pull the changes from git. Since the GitHub repo is public, we don't have to use any private access tokens. Then, we use Quartz to build our page.


```yml
services:
  git-sync:
    image: openweb/git-sync:0.0.1
    environment:
      GIT_SYNC_REPO: https://github.com/AldeRoberge/AGX-Wiki.git
      GIT_SYNC_DEST: /vault
      GIT_SYNC_BRANCH: main
      GIT_SYNC_REV: FETCH_HEAD
      GIT_SYNC_WAIT: "10"
    volumes:
      - ./vault:/vault
    restart: always
  quartz:
    image: shommey/dockerized-quartz
    container_name: quartz-notes
    environment:
      BUILD_UPDATE_DELAY: 30
      AUTO_REBUILD: true
      REBUILD_WEBHOOK_SECRET: topsecretrebuildstuff
      GIT_REPO: https://github.com/AldeRoberge/AGX-Wiki-Quartz.git
    volumes:
      - ./vault:/vault:ro
    ports:
      - 8888:80
    restart: unless-stopped
networks: {}
```



> [!warning]
> We have 'AUTO_REBUILD' enabled, but I didn't find it to work with git-sync. So I'm manually restarting the docker container so that it builds the wiki. It's not optimal (can have downtime), but since it takes a few seconds, it's fine.