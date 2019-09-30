# Containers - Docker

* Example application is nodejs simple express (http-app) which provides http endpoint (/ and /api) also a GET request (/api) according internal interval.

Create container image

```bash
#!/bin/bash
docker build -t http-app .
```

Verify created image

```bash
#!/bin/bash
docker images | grep http-app
```

Run created image

```bash
#!/bin/bash
docker run --name http-app -p 3000:3000/tcp http-app:latest
```

---

# Create local container registry

Tag container image

```bash
#!/bin/bash
docker tag http-app localhost:5000/http-app:latest
```

Create local container registry

```bash
#!/bin/bash
docker run -d -p 5000:5000 --restart=always --name registry registry:2
```

Push container image to local container registry

```bash
#!/bin/bash
docker push localhost:5000/http-app
```

Verify local container registry

```bash
#!/bin/bash
curl localhost:5000/v2/_catalog
```
