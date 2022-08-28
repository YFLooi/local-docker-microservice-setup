# Logigng setup
# Pre-requisite
## Setup for fluentd
(Link)[https://opensearch.org/docs/latest/opensearch/install/important-settings/]
Increase the Maximum Number of File Descriptors to  at least 65536
Run `ulimit -n`
If less than 65536, add the following lines to `/etc/security/limits.conf` and reboot:
```
root soft nofile 65536
root hard nofile 65536
* soft nofile 65536
* hard nofile 65536
```
For high load environments with many Fluentd instances, add the following configuration to your `/etc/sysctl.conf` file:
```
net.core.somaxconn = 1024
net.core.netdev_max_backlog = 5000
net.core.rmem_max = 16777216
net.core.wmem_max = 16777216
net.ipv4.tcp_wmem = 4096 12582912 16777216
net.ipv4.tcp_rmem = 4096 12582912 16777216
net.ipv4.tcp_max_syn_backlog = 8096
net.ipv4.tcp_slow_start_after_idle = 0
net.ipv4.tcp_tw_reuse = 1
net.ipv4.ip_local_port_range = 10240 65535
```
Implement by running `sysctl -p ` or rebooting machine

## Setup for Opensearch
(Link)[https://opensearch.org/docs/latest/opensearch/install/important-settings/]
1. Make sure the Linux setting vm.max_map_count is set to at least 262144.
To check amount set: `cat /proc/sys/vm/max_map_count`
To increase value:
- Edit `/etc/sysctl.conf` and add the line `vm.max_map_count=262144`

- Then run `sudo sysctl -p` to reload.

# Setup to run log collection with Opensearch
1. From a terminal in this repo's root folder, start with the following command:
   ```
    docker-compose -f docker-compose.local-microservices.yml \
    -f ./logging-setup/docker-compose.yml \
    up --env-file .env up

   ```
   Use `up --detach` to run all this in background
   `--env-file` flag is useful for env variables that apply to all repos
2. Access opensearch dashboard at http://localhost:5601
3. Stop with `docker-compose down -v`. `-v` removes all images created

# Use with non-standard docker-compose file names
The key is to use `-f` (file flag) to Ex of commands:
1. Starting docker-compose
   `docker-compose -f docker-compose.gamification.yml up`
2. Stopping docker-compose
   `docker-compose -f docker-compose.gamification.yml down -v`

