# NELK Stack Docker Compose App

* Author: [Jonathan M. Wilbur](https://jonathan.wilbur.space) <[jonathan@wilbur.space](mailto:jonathan@wilbur.space)>
* Copyright Year: 2018
* License: [MIT License](https://mit-license.org/)

Nginx, ElasticSearch, LogStash, and Kibana (NELK) in a Docker-Compose App.

This one proxies Kibana behind Nginx and uses HTTP Basic Authentication over
TLS, so you can expose Kibana to the public Internet safely, after using valid
TLS certificates and changing the credentials (described below).

**WARNING: LogStash is NOT proxied, and therefore not secured with TLS, nor protected by a password. It will be exposed to the public Internet if you run this on a connected host that is not behind a network-based firewall.**

## Usage

Run `docker-compose up`, and give it a minute or two to build and boot.

Log into Kibana via `https://localhost:4443/`.

The default credentials are:

- Username: `squishy`
- Password: `30z0dtu8`

In production, delete these credentials from `./data/nginx/htpasswd`. Generate
new ones using this command:

```bash
printf "USER:$(openssl passwd -crypt PASSWORD)\n"
```

You should also generate a valid key-certificate pair in `./configuration/nginx`,
but I'm not your mother.

## Curator

This stack also comes with [Curator](https://github.com/elastic/curator) almost
ready to go. To use it, simply uncomment it from the `docker-compose.yml` file
and edit the configuration files in `./configuration/curator/`.

**WARNING: Curator is literally a tool for deleting old ElasticSearch entries. If you misconfigure it, you could delete wanted data.**

## ToDo

- [x] Curator
- [x] HealthCheck
- [ ] LetsEncrypt (Pending experimentation)
- [ ] Kubernetes Equivalent
- [ ] Docker Swarm Equivalent
- [x] Restart Rules
- [ ] Capability Dropping
- [ ] Put LogStash and ElasticSearch on a separate network
- [ ] Use `configs` instead of volumes where appropriate
- [ ] Add `deploy` configuration?
- [ ] Add `dns_search` (if a `DOMAIN` environment variable can be used effectively)
- [ ] Use `init: false` in each service, just to be explicit
- [ ] Add `labels`
- [ ] Add explicit `/tcp` to published ports
- [ ] Add Production SysCtl requirements for ElasticSearch

## Privacy

Telemetry is off by default, but if that changes, information can be found
[here](https://www.elastic.co/legal/telemetry-privacy-statement).

## Contact Me

If you would like to suggest fixes or improvements on this library, please just
[leave an issue on this GitHub page](https://github.com/JonathanWilbur/asn1-ts/issues). If you would like to contact me for other reasons,
please email me at [jonathan@wilbur.space](mailto:jonathan@wilbur.space)
([My GPG Key](https://jonathan.wilbur.space/downloads/jonathan@wilbur.space.gpg.pub))
([My TLS Certificate](https://jonathan.wilbur.space/downloads/jonathan@wilbur.space.chain.pem)). :boar: