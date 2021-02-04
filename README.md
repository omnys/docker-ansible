# Docker with ansible

Inspired by: https://github.com/willhallonline/docker-ansible

An "ansible" user is created inside the container and used to execute commands.
Change the "/home/user" path with your local environment.

## Run in interactive mode

```console
docker run  --rm -it \
    --mount type=bind,source="$(pwd)",target=/ansible \
    --mount type=bind,source=/home/user/.ssh,target=/home/ansible/.ssh \
    omnys/ansible:2.8.17 \
    bash
```

## Run a playbook

```console
docker run  --rm -it \
    --mount type=bind,source="$(pwd)",target=/ansible \
    --mount type=bind,source=/home/user/.ssh,target=/home/ansible/.ssh \
    omnys/ansible:2.8.17 \    
    ansible-playbook playbook.yml
```

## Execute aws cli cmd from ansible

If you need to execute aws cli commands, and you want to load local aws profiles, add a custom mount:

```console
... --mount type=bind,source=/home/user/.aws,target=/home/ansible/.aws ...
```

## Share the ssh agent socket with the container

```console
... --volume $SSH_AUTH_SOCK:/ssh-agent --env SSH_AUTH_SOCK=/ssh-agent ...
```
