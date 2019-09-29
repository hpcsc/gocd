## GoCD Setup Using Docker Compose

This repository uses `docker-compose` to setup a testing environment with one GoCD server and 3 GoCD agents

### First time setup

#### Starting docker-compose

```
docker-compose up -d
```

The docker-compose file contains one server and three agents:
- Server is from official GoCD github page: [https://github.com/gocd/docker-gocd-server](https://github.com/gocd/docker-gocd-server)
- 3 GoCD agents that are based on Docker DinD image [https://hub.docker.com/r/gocd/gocd-agent-docker-dind](https://hub.docker.com/r/gocd/gocd-agent-docker-dind)

Note:
- The server and agents will take a while to initialize and startup correctly. GoCD agents will automatically register with GoCD server (however agents need to be enabled from server UI before they can be used for any pipeline).
- GoCD server can be accessed through: `http://localhost:8153`
- Local git server can be accessed through: `http://localhost:3000`
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
