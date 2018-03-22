## GoCD Setup Using Docker Compose

This repository uses `docker-compose` to setup a testing environment with one GoCD server and several GoCD agents (Ubuntu 16.04)

### First time setup

#### Starting docker-compose

```
docker-compose up
```

The docker-compose file contains one server and three agents:
- Server is from official GoCD github page: [https://github.com/gocd/docker-gocd-server](https://github.com/gocd/docker-gocd-server)
- 2 agents that based on official GoCD agent docker image and install Docker CE on top: [https://github.com/hpcsc/gocd-agent-dind](https://github.com/hpcsc/gocd-agent-dind)
- 1 agent with Docker CE and .NET Core SDK installed: [https://github.com/hpcsc/gocd-agent-dotnet](https://github.com/hpcsc/gocd-agent-dotnet)

Note:
- The server and agents will take a while to initialize and startup correctly. GoCD agents will automatically register with GoCD server.
- GoCD server can be accessed through: `http://localhost:8153`
- Local git server can be accessed through: `http://localhost:3000`
- All agent images have Docker CLI installed. However they use Docker socket from the host machine (by mounting `/var/run/docker.sock` from host machine to their own volume) so all containers created by the agents will be in host machine Docker. This idea is from [https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/](https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/)
- This is NOT production setup

#### Setting up local Git server (gogs)

Open local git server at http://localhost:3000

Setup with following settings:

- Database Type: PostgreSQL
- Host: git-repo-db:5432
- User: postgres
- Password: postgrespw
- Database Name: postgres

The remaining leave as default. 

Expand Admin Account Settings, fill in information to create an admin account

Click 'Install Gogs'
