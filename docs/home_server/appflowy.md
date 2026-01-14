# AppFlowy


## How to install with docker

[Local Host Deployment](https://appflowy.com/docs/Local-Host-Deployment)

### Known issues
- [Unable to connect to server](https://github.com/AppFlowy-IO/appflowy/issues/8358)


In my case in `docker logs appflowy-cloud-admin_frontend-1` I had:
```
[18:33:28] 🚨 [ServerFetch] [CRITICAL] Server fetch failed: {
  name: 'GoTrue login',
  url: 'http://localhost/gotrue/token?grant_type=password',
  method: 'POST',
  error: {
    name: 'TypeError',
    message: 'fetch failed',
...
```
I only had to change in `.env`:
`FQDN=<your_machine_ip>:<port>`
In my case it was(because I changed NGINX_PORT=4080):
`FQDN=192.168.0.64:4080`

After that `docker logs appflowy-cloud-admin_frontend-1`:
```
...
 ✓ Starting...
 ✓ Ready in 280ms

```


### [NOT WORKING] Backup 
https://appflowy.com/docs/Using-External-PostgreSQL


Dump the existing database
```
docker exec -t appflowy-cloud-postgres-1 pg_dump -U postgres postgres > appflowy_backup.sql
```

Backup minio
```
docker run --rm \
  -v appflowy-cloud_minio_data:/data \
  -v $(pwd):/backup \
  alpine tar czf /backup/minio.tar.gz -C /data .

```


Restore postgres
```
cat appflowy_backup.sql | docker exec -i appflowy-cloud-postgres-1   psql -U postgres postgres
```

Restore minio
```
docker run --rm \
  -v appflowy-cloud_minio_data:/data \
  -v $(pwd):/backup \
  alpine sh -c "cd /data && tar xzf /backup/minio.tar.gz"
```