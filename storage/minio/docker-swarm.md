```
version: '3.7'
services:
  minio1:
    hostname: minio1
    image: quay.io/minio/minio:RELEASE.2023-03-09T23-16-13Z
    command: server --console-address ":9001" http://minio{1...2}/data
    # ports:
    #   - "9000:9000"
    #   - "9001:9001"
    environment:
      MINIO_ROOT_USER: minio
      MINIO_ROOT_PASSWORD: Minio!@#123
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9000/minio/health/live"]
      interval: 30s
      timeout: 20s
      retries: 3
    deploy:
      #mode: global
      placement:
        constraints:
          - "node.labels.minio==minio1"
      restart_policy:
        condition: on-failure
    volumes:
      - /data:/data
    networks:
      - minio

  minio2:
    hostname: minio2
    image: quay.io/minio/minio:RELEASE.2023-03-09T23-16-13Z
    command: server --console-address ":9001" http://minio{1...2}/data
    # ports:
    #   - "9000:9000"
    #   - "9001:9001"
    environment:
      MINIO_ROOT_USER: minio
      MINIO_ROOT_PASSWORD: Minio!@#123
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9000/minio/health/live"]
      interval: 30s
      timeout: 20s
      retries: 3
    deploy:
      #mode: global
      placement:
        constraints:
          - "node.labels.minio==minio2"
      restart_policy:
        condition: on-failure
    volumes:
      - /data:/data
    networks:
      - minio

  nginx:
    image: nginx:1.19.2-alpine
    hostname: nginx
    volumes:
      - /srv/nginx/nginx.conf:/etc/nginx/nginx.conf:ro
    ports:
      - "9000:9000"
      - "9001:9001"
    depends_on:
      - minio1
      - minio2
    deploy:
      replicas: 1
      restart_policy:
        condition: on-failure
      resources:
        limits:
          cpus: '0.50'
          memory: 100M
    networks:
      - minio
networks:
  minio:
    driver: overlay
    name: minio
    attachable: true
```
* for more info check this [link](https://github.com/minio/minio/tree/master/docs/orchestration/docker-compose).

---
* Remember that if we recreate the service again.. because minio's directory (.minio.sys) is full of the previous config contents, we need to stop minio servers, delete the directory and then start it again.  

--
