# Install and test Docker

## Install Docker
1. Being lazy tonight. Just go [here](https://docs.docker.com/docker-for-mac/) and click download. I'll assume everything went peachy.

## Test Docker

1. Download this repository `git clone git@github.com:grantbachman/kubernetes-tutorial.git`
2. `cd kubernetes-tutorial/example/`
3. Build a docker image.

   `docker build -t api .`

  This command tells docker to build an image (`docker build`) tagged with a name (`-t api`) using the current directory (`.`).
4. Run a container based on the image we just built.

    `docker run -p 1234:5000 api`

    This command tells docker to:
      * run a container (`docker run`)
      * publish the container's port 5000 to the host machine's port 1234 (`-p 1234:5000`).
        * By default, docker containers run in isolation, so you won't be able to access the application from the outside world. Since the container's application is running on port 5000 we need to tell docker to expose that port so the host machine (my laptop) can access it.
        * If you only tell docker to expose the port but don't specify which port it should be published as, it'll pick a random one. You can figure out which port it's published as by running `docker ps` to get the Container ID, then `docker inspect $CONTAINER_ID`, and looking at *NetworkSettings*
      * run the container from the image called `api`

5. Visit [localhost:1234](localhost:1234). You should see a message saying *Flask Dockerized*. If you see this message then you're good to go with Docker!

