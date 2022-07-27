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
