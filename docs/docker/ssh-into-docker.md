---
author: ''
category: Docker
date: '2020-04-20'
summary: ''
title: Ssh Into Docker
---
## SSH Into Docker

View running containers:

    docker ps

SSh into the container:

    docker exec -it <contianer_id> /bin/bash
    
of

    docker exec -it <contianer_id> /sh
