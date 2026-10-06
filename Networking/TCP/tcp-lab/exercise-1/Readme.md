## Build the Environment

**Step 1:** Create directory
``` mkdir tcp-lab
    cd tcp-lab
```

**Step 2:** Create docker compose file
``` touch docker-compose.yml
    vi docker-compose.yml
```
Copy the code from shared docker-compose.yml in your docker compose file.

**Step 3:** Start the docker containers
```
docker compose up -d
```

**Step 4:** Check for running docker containers
```
docker ps
```
you should have: 
- ubuntu_client
- ubuntu_server