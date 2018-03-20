## GoCD Setup Using Docker Compose

This repository uses `docker-compose` to setup a testing environment with one GoCD server and one GoCD agent (Ubuntu 16.04)

Both images are from official GoCD github pages:
- [https://github.com/gocd/docker-gocd-server](https://github.com/gocd/docker-gocd-server)
- [https://github.com/gocd/docker-gocd-agent](https://github.com/gocd/docker-gocd-agent)

### docker-compose.dotnet.yml

```
docker-compose -f docker-compose.dotnet.yml up
```

This docker-compose file contains one server and one agent with .NET Core SDK installed

Note:
- The agent image has Docker CLI installed. However it uses Docker socket from the host machine (by mounting `/var/run/docker.sock` from host machine to its own volume) so all containers created by the agent will be in host machine Docker. This idea is from [https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/](https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/)

### docker-compose.yml

```
docker-compose up
```

This docker-compose file contains one server and three agents:
- 2 agents from official GoCD image
- 1 agent with .NET Core SDK installed

Note:
- The server and agent will take a while to initialize and startup correctly. GoCD agent will automatically register with GoCD server.
- GoCD server can be accessed through: `http://localhost:8153`
