# Docker with ansible

An "ansible" user is created inside the container and used to execute commands.
Change the "/home/user" path with your local environment.

## Run in interactive mode
docker run  --rm -it \
    --mount type=bind,source="$(pwd)",target=/ansible \
    --mount type=bind,source=/home/user/.ssh,target=/home/ansible/.ssh \
    omnys/ansible:2.8 \
    bash

## Run a playbook
docker run  --rm -it \
    --mount type=bind,source="$(pwd)",target=/ansible \
    --mount type=bind,source=/home/user/.ssh,target=/home/ansible/.ssh \
    omnys/ansible:2.8 \    
    ansible-playbook playbook.yml