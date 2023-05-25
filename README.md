# Nodemotion setup


## Setup locally

Run docker

```bash
docker-compose --env-file=.env.dev -f docker-compose.yml up
```

## Setup on server

Install and start [portainer.io](https://www.portainer.io/)

1. Setup portainer volume
    ```
    docker volume create portainer_data
    ```

2. Start portainer
    ```
    docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
    ```

3. Go through portainer wizard and create admin account

4. Create a new stack app from git repository
    
    1. Go to local machine node
    1. Go to stacks tab
    1. Press `Add stack`
    1. Choose Repository option
    1. Type repository URL (i.e. this repository URL)
    1. Type repository reference i.e. `refs/heads/master`
    1. Set automatic updates
    1. Setup environment variables as in `.env.dev` - adjust values to your setup
    1. Press `Deploy the stack`

