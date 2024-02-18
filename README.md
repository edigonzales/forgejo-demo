# forgejo-demo

## Ausprobieren
- Disable Self-Registration: Wie werden neue Benutzer angelegt?
- OpenID?
- Captacha?
- Email?

- Wie / was genau mounten? `/var/lib/gitea`
- ssh port?
- Verhindern, dass Runner missbraucht werden? keine pull-requests? kein branchen?




## foo

Auf den ersten Blick kann ein fremder Habasch die Action mit einem Pullrequest eines geforkten Repos nicht auslösen.

- These configuration options will be written into: /etc/gitea/app.ini
- superuser / BLum6@P!z2Vp4dP

- edigonzales / eQW5$uf$U$r$6Y9


codeberg action runner r7nAnnpubiwtPc3KTXan3jEADwqAgPOvbUPEZGvk

adduser runner
gruppe...
sudo service docker restart

$ docker run -v /var/run/docker.sock:/var/run/docker.sock  -v $PWD:/data --rm code.forgejo.org/forgejo/runner:3.3.0 forgejo-runner register --no-interactive --token r7nAnnpubiwtPc3KTXan3jEADwqAgPOvbUPEZGvk --name forgejo-runner --instance https://codeberg.org 


runner@docker-ce-ubuntu-4gb-nbg1-1:~$ docker run -v /var/run/docker.sock:/var/run/docker.sock  -v $PWD:/data --rm code.forgejo.org/forgejo/runner:3.3.0 forgejo-runner register --no-interactive --token v0bVRhOPsweF1nMBEYPIBkehxkSRM4Ctib95lSSd --name forgejo-runner --instance https://codeberg.org
level=info msg="Registering runner, arch=amd64, os=linux, version=v3.3.0."
level=warning msg="Runner in user-mode."
level=debug msg="Successfully pinged the Forgejo instance server"
level=info msg="Runner registered successfully."


docker run -v /var/run/docker.sock:/var/run/docker.sock  -v $PWD:/data --rm code.forgejo.org/forgejo/runner:3.3.0 forgejo-runner generate-config > config.yml


docker run -v /var/run/docker.sock:/var/run/docker.sock --user 1000:996 -v $PWD:/data --rm code.forgejo.org/forgejo/runner:3.3.0 forgejo-runner --config config.yml daemon

docker run -d -v /var/run/docker.sock:/var/run/docker.sock --user 1000:996 -v $PWD:/data --rm code.forgejo.org/forgejo/runner:3.3.0 forgejo-runner --config config.yml daemon


```
version: "3"

services:

  docker:
    image: docker:dind
    privileged: true
    volumes:
      - certs:/certs

  runner:
    image: code.forgejo.org/forgejo/runner:3.3.0
    environment:
      DOCKER_HOST: tcp://docker:2376
      DOCKER_TLS_VERIFY: 1
      DOCKER_CERT_PATH: /certs/client
    volumes:
      - $PWD:/data
      - certs:/certs
    command: "forgejo-runner --config config.yml daemon"
volumes:
    certs:

```
