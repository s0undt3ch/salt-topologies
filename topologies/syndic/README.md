# Syndic Topology Example

## Build Base Image

```
docker build --rm -t syndic-topology-base -f Dockerfile.base.centos .
```

## Build Docker Compose Images

```
docker-compose build
```

## Run The Example

### Bring All Containers Up
```
docker-compose up -d
```

### Terminal 1 - Logs From mom
```
docker exec -it mom tail -f /var/log/salt/master
```

### Terminal 2 - Logs From syndic-master
```
docker exec -it syndic-master multitail /var/log/salt/master /var/log/salt/minion /var/log/salt/syndic
```

### Terminal 3

#### Ping Minions Connected To syndic-master
```
docker exec -it syndic-master salt '*' test.ping
```

##### Expected Output
```
minion-2:
    True
syndic-master:
    True
```

#### Ping Minions Connected To mom
```
docker exec -it mom salt '*' test.ping
```

##### Expected Output
```
minion-1:
    True
syndic-master:
    True
minion-2:
    True
```
