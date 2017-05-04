## GoCD Setup Using Docker Compose

This repository uses `docker-compose` to setup a testing environment with one GoCD server and one GoCD agent (Ubuntu 16.04)
Both images are from official GoCD github pages:
- [https://github.com/gocd/docker-gocd-server](https://github.com/gocd/docker-gocd-server)
- [https://github.com/gocd/docker-gocd-agent](https://github.com/gocd/docker-gocd-agent)

### Start With Original Agent
```
docker-compose up
```
Note:
- The server and agent will take a while to initialize and startup correctly. GoCD agent will automatically register with GoCD server.
- GoCD server can be accessed through: `http://localhost:8153`

### Start With Agent Having .NET Core SDK Installed
```
docker-compose -f docker-compose.dotnet.yml up
```
