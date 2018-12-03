# ELK Stack Docker Compose App

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

- [ ] APM Server?
- [ ] Curator?
- [ ] LogSpout?
- [ ] HealthCheck?