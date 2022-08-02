# mac-workstation.provisioning

[![default](https://github.com/mazgi/mac-workstation.provisioning/actions/workflows/default.yml/badge.svg)](https://github.com/mazgi/mac-workstation.provisioning/actions/workflows/default.yml)

## How to run

1st, you should get up the provisioning service via docker-compose and hold the terminal for the service.
Or, you are able to use the option `-d` or `--detach` with that up.

```console
docker-compose up
```

Now, in another terminal, you are able to access the provisioning container via `docker-compose exec` command.

```console
docker-compose exec provisioning zsh -l
```

Next, I recommend exporting several environment variables to access your new Mac from the provisioning service easily.

```console
export TARGET_HOSTNAME=YOUR_VALUE
export TARGET_OS_USER=YOUR_VALUE
```

You are able to resolve the FQDN as has suffix `.local` via the `dig @224.0.0.251 -p 5353` command if you are using an OS that is enabled mDNS services, such as Bonjour, or Avahi.
In this case, the DNS server `224.0.0.251` is a unique fixed IP address for mDNS and the correct IP address in all environments.

```console
docker-compose exec provisioning ansible -m raw -a hostname -i $(dig +short @224.0.0.251 -p 5353 ${TARGET_HOSTNAME}.local), -u ${TARGET_OS_USER} all
```

```console
docker-compose exec provisioning ansible -m gather_facts -i $(dig +short @224.0.0.251 -p 5353 ${TARGET_HOSTNAME}.local), -u ${TARGET_OS_USER} all
docker-compose exec provisioning ansible -m gather_facts -a "filter=ansible_machine" -i $(dig +short @224.0.0.251 -p 5353 ${TARGET_HOSTNAME}.local), -u ${TARGET_OS_USER} all
docker-compose exec provisioning ansible -m gather_facts -a "filter=ansible_default_ipv4.address" -i $(dig +short @224.0.0.251 -p 5353 ${TARGET_HOSTNAME}.local), -u ${TARGET_OS_USER} all
```
