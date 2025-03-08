## Restart Podman

```sh
wsl --shutdown
wsl --list --verbose
wsl --unregister podman-machine-default
wsl --unregister docker-desktop
```

## Find What is Using Port 80

### Docker:

```sh
docker ps --format "table {{.ID}}\t{{.Image}}\t{{.Ports}}"
```

### Other:

```sh
sudo netstat -tulnp | grep :80
```

---

## How to Completely Stop NGINX

### Check if it's Running

```sh
sudo systemctl status nginx
```

### Stop It

```sh
sudo systemctl stop nginx
```

### Disable it from Starting on Boot

```sh
sudo systemctl disable nginx
```

---

## How to Read Logs from Server

### Connect to the Server

```sh
ssh root@5.181.218.248
```

### Find Running Containers

```sh
docker ps
```

### See Logs in Real-Time

```sh
docker logs -f user-agx.world.server-1
```

---

## How to Restart (docker-compose file is in `/home/user`)

```sh
cd /home/user/
docker-compose down && docker-compose up -d
```

---

## How to Create `.env` File

```sh
cd /home/user

touch .env
```

**Note:** Files starting with a dot (`.`) are hidden by default. Use the following command to see them:

```sh
ls -a
```