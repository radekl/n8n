# Nodemotion setup


## Setup locally

Run docker

```bash
docker-compose --env-file=.env.dev -f docker-compose.yml -f docker-compose-dev.yml up
```


## Setup on server

0. Clone repository to `/etc/docker-compose/n8n` directory:

    ```bash
    docker run -v /etc/docker-compose/:/workdir -w /workdir cmd.cat/git git clone https://github.com/radekl/n8n.git
    ```

1. Create `cert/ovh.ini` with contents:

    ```ini
    # OVH API credentials used by Certbot
    dns_ovh_endpoint = ovh-eu
    dns_ovh_application_key = MDAwMDAwMDAwMDAw
    dns_ovh_application_secret = MDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAw
    dns_ovh_consumer_key = MDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAw
    ```
2. Create `.env` file with contents:

    ```bash
    DB_PASSWORD=generate_random_password_for_db
    PUBLIC_DNS=your.domain.here
    ```

3. Link file `etc/systemd/system/docker-compose@.service` to `/etc/systemd/system/docker-compose@.service`

    ```bash
    ln -s /etc/docker-compose/n8n/etc/systemd/system/docker-compose@.service /etc/systemd/system/docker-compose@.service
    ```

4. Reload systemd daemon: `systemctl daemon-reload`
5. Enable n8n app `systemctl enable docker-compose@n8n`
6. Start n8n app `systemctl start docker-compose@n8n`
7. Verify that your app works on a domain you've chosen.
