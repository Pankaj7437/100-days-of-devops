# 🚀 Create Docker Bridge Network

## 📌 Objective

Create a Docker network named **media** on **App Server 3 (stapp03)** with:

* Driver: `bridge`
* Subnet: `10.10.1.0/24`
* IP Range: `10.10.1.0/24`

---

# 🖥️ Environment Details

| Component    | Value                  |
| ------------ | ---------------------- |
| Server       | App Server 3 (stapp03) |
| Network Name | media                  |
| Driver       | bridge                 |
| Subnet       | 10.10.1.0/24           |
| IP Range     | 10.10.1.0/24           |

---

# 🔹 Step 1: Connect to App Server 3

```bash
ssh banner@stapp03
```

---

# 🔹 Step 2: Create Docker Network

```bash
docker network create \
-d bridge \
--subnet=10.10.1.0/24 \
--ip-range=10.10.1.0/24 \
media
```

### Explanation

| Option                    | Purpose                          |
| ------------------------- | -------------------------------- |
| `docker network create`   | Creates a new Docker network     |
| `-d bridge`               | Uses the bridge network driver   |
| `--subnet=10.10.1.0/24`   | Defines the network subnet       |
| `--ip-range=10.10.1.0/24` | Defines the allocatable IP range |
| `media`                   | Network name                     |

---

# 🔹 Step 3: Verify Network Creation

```bash
docker network ls
```

Expected:

```text
NETWORK ID     NAME      DRIVER
xxxxxxxxxx     media     bridge
```

---

# 🔹 Step 4: Inspect Network Configuration

```bash
docker network inspect media
```

Important output:

```json
{
  "Name": "media",
  "Driver": "bridge",
  "IPAM": {
    "Config": [
      {
        "Subnet": "10.10.1.0/24",
        "IPRange": "10.10.1.0/24"
      }
    ]
  }
}
```

---

# 📖 Command Breakdown

### Create Bridge Network

```bash
docker network create -d bridge --subnet=10.10.1.0/24 --ip-range=10.10.1.0/24 media
```

Creates a custom bridge network that containers can later attach to for isolated communication.

---

# 🔍 Verification Commands

```bash
docker network ls

docker network inspect media
```

Verify:

* Network name is `media`
* Driver is `bridge`
* Subnet is `10.10.1.0/24`
* IPRange is `10.10.1.0/24`

---

# ⚡ Commands Used

```bash
ssh banner@stapp03

docker network create \
-d bridge \
--subnet=10.10.1.0/24 \
--ip-range=10.10.1.0/24 \
media

docker network ls

docker network inspect media
```

---

# ✅ Result

Successfully created the Docker network **media** on **App Server 3** using the **bridge** driver and configured it with subnet **10.10.1.0/24** and IP range **10.10.1.0/24**. Verification using `docker network inspect media` confirmed the configuration.
