# Como instalar thingsboard em meu PC ?

### Pre-requisitos para seu Ubuntu <a id="prerequisites"></a>

* [Install Docker CE](https://docs.docker.com/engine/installation/)

### Running  <a id="running"></a>

```text
$ docker run -it -p 9090:9090 -p 1883:1883 -p 5683:5683/udp -v ~/.mytb-data:/data -v ~/.mytb-logs:/var/log/thingsboard --name mytb --restart always thingsboard/tb-postgres
```

Where:

* `docker run` - run this container
* `-it` - attach a terminal session with current ThingsBoard process output
* `-p 9090:9090` - connect local port 9090 to exposed internal HTTP port 9090
* `-p 1883:1883` - connect local port 1883 to exposed internal MQTT port 1883
* `-p 5683:5683` - connect local port 5683 to exposed internal COAP port 5683
* `-v ~/.mytb-data:/data` - mounts the host’s dir `~/.mytb-data` to ThingsBoard DataBase data directory
* `-v ~/.mytb-logs:/var/log/thingsboard` - mounts the host’s dir `~/.mytb-logs` to ThingsBoard logs directory
* `--name mytb` - friendly local name of this machine
* `--restart always` - automatically start ThingsBoard in case of system reboot and restart in case of failure.
* `thingsboard/tb-postgres` - docker image, can be also `thingsboard/tb-cassandra` or `thingsboard/tb`

After executing this command you can open `http://{your-host-ip}:9090` in you browser \(for ex. `http://localhost:9090`\). You should see ThingsBoard login page. Use the following default credentials:

* **Systen Administrator**: sysadmin@thingsboard.org / sysadmin
* **Tenant Administrator**: tenant@thingsboard.org / tenant
* **Customer User**: customer@thingsboard.org / customer

You can always change passwords for each account in account profile page.

FONTE: [https://thingsboard.io/docs/user-guide/install/docker/](https://thingsboard.io/docs/user-guide/install/docker/)



