# Secure-session-vault

A secure client-side vault for storing session data outside of localStorage or sessionStorage using self-hosting with docker.
Designed to work with a self-hosted Dockerized backend that protects sensitive data from XSS and other client-side attacks.

[![npm downloads](https://img.shields.io/npm/dm/secure-session-vault-client)](https://www.npmjs.com/package/secure-session-vault-client)

<br/>

[![NPM](https://nodei.co/npm/secure-session-vault-client.png)](https://nodei.co/npm/secure-session-vault-client/)

## 🔐 Features

- Stores session tokens securely via a local vault microservice.
- Avoids `localStorage`/`sessionStorage` vulnerabilities.
- ESM compatible, reusable NPM package.
- Auto-discovers Docker-hosted vault via default hostnames or manual URL injection.
- Self-hosting with docker.

## 🚀 Installation

```bash
npm install secure-session-vault-client
 OR
 yarn add secure-session-vault-client
 OR
 pnpm install secure-session-vault-client
```

## ⚙️ Vault Backend
Run the backend using Docker, the backend is available on docker hub at[Docker Hub](https://hub.docker.com/r/ethernmyth/secure-session-vault):

```bash
docker run -p 17000:17000 ethernmyth/secure-session-vault:latest
```

Or include it in your Docker Compose setup with:

```yaml
services:
  vault:
    image: ethernmyth/secure-session-vault:latest
    ports:
      - "17000:17000"
```

## 🛠️ Usage

This was built with access for node supported project and the backend can be accessed independently as well:

```typescript
import { SecureSessionVault } from "secure-session-vault-client";

const vault = new SecureSessionVault(); // Or pass a custom vault URL

await vault.setItem("accessToken", "abc123");
const token = await vault.getItem("accessToken");
await vault.removeItem("accessToken");
```

2. **Access the Vault API**

Store a value:

```bash
curl -X POST "http://localhost:17000/vault?key=session&value=abc123"
```

Retrieve it:

```bash
curl "http://localhost:17000/vault?key=session"
```

Delete it:

```bash
curl -X DELETE "http://localhost:17000/vault?key=session"
```

## 🌐 Default Fallback URLs
The client will try the following in order:

http://localhost:17000

http://127.0.0.1:17000

http://host.docker.internal:17000

---

You can override with:

```typescript
new SecureSessionVault("http://custom-ip-or-host:17000");
```


## 👤 Author

Created and Maintained by: [Ethern-Myth](https://github.com/ethern-myth)

---

**Give a like to this project and let's share it and spread it more. Thanks.**





