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

On Windows, you have to set the `PWD` environment variable. From PowerShell,
run `$env:PWD=$PWD` prior to starting the stack.

Run `docker-compose up`, and give it a minute or two to build and boot.

Log into Kibana via `https://localhost:4443/`.

The default credentials are:

- Username: `squishy`
- Password: `L+ZyfiS6`

In production, delete these credentials from `./data/nginx/htpasswd`. Generate
new ones using this command:

```bash
printf "USER:$(openssl passwd -crypt PASSWORD)\n"
```

You should also generate a valid key-certificate pair in `./configuration/nginx`,
but I'm not your mother.

Finally, set the domain in `.env`, if you please. It is not mandatory.

## Curator

This stack also comes with [Curator](https://github.com/elastic/curator) almost
ready to go. To use it, simply uncomment it from the `docker-compose.yml` file
and edit the configuration files in `./configuration/curator/`.

**WARNING: Curator is literally a tool for deleting old ElasticSearch entries. If you misconfigure it, you could delete wanted data.**

## Troubleshooting

- On Windows, you have to set the `PWD` environment variable. From PowerShell,
  run `$env:PWD=$PWD`.
- If you are running this on a Windows machine, know that Hyper-V, which Docker
  uses, reserves large ranges of TCP ports, even when they are not in use. If
  you are finding that a container will anomalously not start because it cannot
  bind on a specific TCP port, even though nothing is listening on it, this may
  be the culprit. See [this GitHub issue](https://github.com/docker/for-win/issues/3171).

## ToDo

- [x] Fix `.gitignore`
- [x] Fix `$PWD` volume-mounting issue
- [ ] Experiment with Nginx LDAP Authentication
- [ ] LetsEncrypt (Pending experimentation)
- [ ] Kubernetes Equivalent
- [ ] Docker Swarm Equivalent

## Privacy

Telemetry is off by default, but if that changes, information can be found
[here](https://www.elastic.co/legal/telemetry-privacy-statement).

## Contact Me

If you would like to suggest fixes or improvements on this library, please just
[leave an issue on this GitHub page](https://github.com/JonathanWilbur/asn1-ts/issues). If you would like to contact me for other reasons,
please email me at [jonathan@wilbur.space](mailto:jonathan@wilbur.space)
([My GPG Key](https://jonathan.wilbur.space/downloads/jonathan@wilbur.space.gpg.pub))
([My TLS Certificate](https://jonathan.wilbur.space/downloads/jonathan@wilbur.space.chain.pem)). :boar: