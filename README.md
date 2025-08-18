# AmneziaWG client for Docker

Run an AmneziaWG peer in a Docker container. Allows routing of specific Docker networks or the entire `host` network (useful for Linux hosts that do not support the AmneziaWG core module).

### Setup

1. Install Docker if you haven't yet:
   ```bash
   curl -sSL https://get.docker.com | sh
   sudo usermod -aG docker $USER
   ```
2. Get an AmneziaWG config

   Generate a .conf file and place it in a new folder somewhere on the host.

3. Run the container

   To run it on a separate Docker network:

   ```bash
   docker run -dit \
    --name=amneziawg-client \
    -v /path/to/dir/with/config:/config \
    --device=/dev/net/tun:/dev/net/tun \
    --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
    --sysctl="net.ipv4.ip_forward=1" \
    --cap-add=NET_ADMIN \
    --cap-add=SYS_MODULE \
    --restart always \
    ghcr.io/zeozeozeo/amneziawg-client
   ```

   If you'd like to have access to the VPN network from the host, make it run on the host network:

   ```bash
   docker run -dit \
    --name=amneziawg-client \
    -v /path/to/dir/with/config:/config \
    --network=host \
    --device=/dev/net/tun:/dev/net/tun \
    --cap-add=NET_ADMIN \
    --cap-add=SYS_MODULE \
    --restart always \
    ghcr.io/zeozeozeo/amneziawg-client
   ```
