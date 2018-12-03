# NELK Stack Docker Compose App

* Author: [Jonathan M. Wilbur](https://jonathan.wilbur.space) <[jonathan@wilbur.space](mailto:jonathan@wilbur.space)>
* Copyright Year: 2018
* License: [MIT License](https://mit-license.org/)

Nginx, ElasticSearch, LogStash, and Kibana (NELK) in a Docker-Compose App.

This one proxies behind Nginx and uses HTTP Basic Authentication by default, so
you can expose this to the public Internet safely.

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

## ToDo

- [ ] ~~APM Server~~ _Not applicable._
- [ ] Curator `bobrik/curator`
- [ ] ~~LogSpout~~ _Not applicable._
- [x] HealthCheck

## Privacy

Telemetry is off by default, but if that changes, information can be found
[here](https://www.elastic.co/legal/telemetry-privacy-statement).

## Contact Me

If you would like to suggest fixes or improvements on this library, please just
[leave an issue on this GitHub page](https://github.com/JonathanWilbur/asn1-ts/issues). If you would like to contact me for other reasons,
please email me at [jonathan@wilbur.space](mailto:jonathan@wilbur.space)
([My GPG Key](https://jonathan.wilbur.space/downloads/jonathan@wilbur.space.gpg.pub))
([My TLS Certificate](https://jonathan.wilbur.space/downloads/jonathan@wilbur.space.chain.pem)). :boar: