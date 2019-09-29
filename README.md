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

##### Gogs utilities scripts

If you prefer command-line over Gogs UI, there are several shell scripts in `scripts` folder to automate the most common operations with Gogs:

- `./scripts/generate-token.sh`: this will create an access token with name `default-access-token` in Gogs to perform operations using Gogs REST API. This script is used internally by the 2 scripts below.
- `./scripts/create-git-repo.sh some-repo`: create git repo in Gogs
- `./scripts/upload-public-key.sh`: upload your default public key at `~/.ssh/id_rsa.pub` to Gogs server. This is so that you can push to Gogs from your host machine using SSH.

These scripts assume following tools are available in your system:

- [jq](https://stedolan.github.io/jq/)
- curl
