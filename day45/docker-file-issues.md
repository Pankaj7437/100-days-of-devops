Exactly. This was a **KodeKloud troubleshooting lab**, and the important learning point was not creating a Dockerfile from scratch—it was **debugging an existing Dockerfile without changing valid configuration or application data**.

# Dockerfile Troubleshooting – Build Failure

## Lab Overview

This KodeKloud lab involved troubleshooting a Docker build failure on **App Server 3** in the **Stratos Datacenter**.

The Nautilus DevOps team had an existing `Dockerfile` under:

```bash
/opt/docker
```

The Dockerfile was already configured with the required Apache, SSL, and application settings. However, some file paths in the `COPY` instructions were incorrect, causing the Docker image build to fail.

The objective was to **identify and correct only the incorrect paths** and successfully build the image without modifying the base image, valid configuration, or application data.

---

## Task Requirements

The requirements were:

* Work on **App Server 3**.
* Find the Dockerfile under `/opt/docker`.
* Troubleshoot the Docker build failure.
* Fix the incorrect paths in the Dockerfile.
* Do not change the base image.
* Do not change valid Apache/SSL configuration.
* Do not modify the existing application files such as `index.html`.
* Successfully build the Docker image.

---

# 1. Connect to App Server 3

From the jump host:

```bash
ssh banner@stapp03
```

Then move to the Docker directory:

```bash
cd /opt/docker
```

Check the available files:

```bash
ls
```

The directory contained:

```text
Dockerfile
certs
html
```

---

# 2. Inspect the Existing Dockerfile

The original Dockerfile contained:

```dockerfile
FROM httpd:2.4.43

RUN sed -i "s/Listen 80/Listen 8080/g" /usr/local/apache2/conf/httpd.conf

RUN sed -i '/LoadModule\ ssl_module modules\/mod_ssl.so/s/^#//g' conf/httpd.conf

RUN sed -i '/LoadModule\ socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//g' conf/httpd.conf

RUN sed -i '/Include\ conf\/extra\/httpd-ssl.conf/s/^#//g' conf/httpd.conf

COPY /server.crt /usr/local/apache2/conf/server.crt

COPY /server.key /usr/local/apache2/conf/server.key

COPY ./index.html /usr/local/apache2/htdocs/
```

The important point was that the existing configuration should **not** be unnecessarily changed.

---

# 3. First Build Attempt

The first build command attempted was:

```bash
docker build --name new -t .
```

Docker returned:

```text
unknown flag: --name
```

### Why?

`docker build` does not use `--name` for naming an image.

The image name is specified using the `-t` option.

Correct syntax:

```bash
docker build -t myapp .
```

---

# 4. Identify the First Path Problem

The build was then attempted with:

```bash
docker build -t myapp .
```

The build failed at:

```text
COPY ./index.html /usr/local/apache2/htdocs/
```

with:

```text
"/index.html": not found
```

The reason was found by checking the directory:

```bash
ls -la
```

The structure was:

```text
/opt/docker
├── Dockerfile
├── certs
│   ├── server.crt
│   └── server.key
└── html
    └── index.html
```

Therefore, `index.html` was not directly inside `/opt/docker`.

It was located at:

```text
/opt/docker/html/index.html
```

---

# 5. Correct the index.html Path

The incorrect instruction was:

```dockerfile
COPY ./index.html /usr/local/apache2/htdocs/
```

It was corrected to:

```dockerfile
COPY ./html/index.html /usr/local/apache2/htdocs/
```

The existing `index.html` itself was **not modified**.

---

# 6. Identify the Certificate Path

After correcting `index.html`, the next build failed on:

```text
COPY /server.key /usr/local/apache2/conf/server.key
```

The directory structure showed that the certificate files were inside:

```text
/opt/docker/certs
```

Checking the directory:

```bash
cd certs
ls
```

showed:

```text
server.crt
server.key
```

Therefore, the Dockerfile paths were incorrect.

---

# 7. Correct the Certificate Paths

The incorrect paths:

```dockerfile
COPY /server.crt /usr/local/apache2/conf/server.crt

COPY /server.key /usr/local/apache2/conf/server.key
```

were corrected to:

```dockerfile
COPY ./certs/server.crt /usr/local/apache2/conf/server.crt

COPY ./certs/server.key /usr/local/apache2/conf/server.key
```

Again, the certificate files themselves were **not changed**.

---

# 8. Final Corrected Dockerfile

The final Dockerfile was:

```dockerfile
FROM httpd:2.4.43

RUN sed -i "s/Listen 80/Listen 8080/g" /usr/local/apache2/conf/httpd.conf

RUN sed -i '/LoadModule\ ssl_module modules\/mod_ssl.so/s/^#//g' conf/httpd.conf

RUN sed -i '/LoadModule\ socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//g' conf/httpd.conf

RUN sed -i '/Include\ conf\/extra\/httpd-ssl.conf/s/^#//g' conf/httpd.conf

COPY ./certs/server.crt /usr/local/apache2/conf/server.crt

COPY ./certs/server.key /usr/local/apache2/conf/server.key

COPY ./html/index.html /usr/local/apache2/htdocs/
```

### What was changed?

Only the three incorrect source paths:

```text
/server.crt
/server.key
./index.html
```

were corrected to:

```text
./certs/server.crt
./certs/server.key
./html/index.html
```

The following were intentionally left unchanged:

* Base image
* Apache configuration
* SSL configuration
* Existing certificates
* Existing `index.html`
* Apache port configuration

---

# 9. Build the Image

From `/opt/docker`:

```bash
docker build -t myapp .
```

The build completed successfully:

```text
[+] Building 10.1s (13/13) FINISHED
```

The final image was created as:

```text
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
myapp        latest    91ea65cf1ca1   10 seconds ago   166MB
```

---

# 10. Verify the Image

Run:

```bash
docker images
```

Expected result:

```text
REPOSITORY   TAG       IMAGE ID       SIZE
myapp        latest    91ea65cf1ca1   166MB
```

This confirms that the Dockerfile was successfully fixed and the image was built.

---

# Troubleshooting Summary

| Problem                     | Cause                                    | Solution                        |
| --------------------------- | ---------------------------------------- | ------------------------------- |
| `unknown flag: --name`      | `docker build` does not support `--name` | Use `docker build -t myapp .`   |
| `index.html: not found`     | File was inside `html/`                  | Changed to `./html/index.html`  |
| `server.key: not found`     | Certificate was inside `certs/`          | Changed to `./certs/server.key` |
| `server.crt` path incorrect | Certificate was inside `certs/`          | Changed to `./certs/server.crt` |

---

# Directory Structure

Final structure:

```text
/opt/docker
│
├── Dockerfile
│
├── certs/
│   ├── server.crt
│   └── server.key
│
└── html/
    └── index.html
```

Docker build context:

```text
/opt/docker
      │
      ├── Dockerfile
      │
      ├── certs/
      │      ├── server.crt ──────► Apache SSL configuration
      │      └── server.key ──────► Apache SSL configuration
      │
      └── html/
             └── index.html ──────► Apache document root
```

---

# Key DevOps Learning

The main lesson from this lab was **Docker build context and relative paths**.

When running:

```bash
docker build -t myapp .
```

the `.` means that `/opt/docker` becomes the Docker **build context**.

Therefore Docker can access files under that directory, such as:

```text
./certs/server.crt
./certs/server.key
./html/index.html
```

but the Dockerfile must reference their actual locations within the build context.

A useful troubleshooting approach is:

```bash
pwd
ls -la
find . -maxdepth 2 -type f
```

before changing a Dockerfile.

---

# Commands Used

```bash
ssh banner@stapp03

cd /opt/docker

ls

cat Dockerfile

docker build -t myapp .

cd certs
ls

cd ../html
ls

cd ..

sudo nano Dockerfile

docker build -t myapp .

docker images
```

---

# Learning Outcome

This lab helped me practice:

* Troubleshooting Docker build failures
* Understanding Docker build context
* Debugging `COPY` instructions
* Working with relative paths in Dockerfiles
* Reading Docker build error messages
* Understanding Docker image naming with `-t`
* Preserving existing application data and valid configuration
* Building and verifying a Docker image successfully

## Key Takeaway

**Don't immediately rewrite a failing Dockerfile. First read the error, inspect the build context, verify the actual file locations, and change only what is broken.**

This is an important real-world DevOps troubleshooting skill.
