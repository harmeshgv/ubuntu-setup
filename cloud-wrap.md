## Cloudflare WARP – Ubuntu Setup

### 1️⃣ Install prerequisites & add repository key

```bash
sudo apt install -y curl gnupg
curl https://pkg.cloudflareclient.com/pubkey.gpg \
  | sudo gpg --yes --dearmor \
  -o /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg
```

### 2️⃣ Add the Cloudflare WARP repository

```bash
echo "deb [signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] \
https://pkg.cloudflareclient.com/ $(lsb_release -cs) main" \
| sudo tee /etc/apt/sources.list.d/cloudflare-client.list
```

### 3️⃣ Install the client

```bash
sudo apt update
sudo apt install -y cloudflare-warp
```

### 4️⃣ Register a new device

```bash
sudo warp-cli registration new
```

### 5️⃣ Connect to WARP

```bash
sudo warp-cli connect
```

### 6️⃣ Verify connection

```bash
warp-cli status
# Expected output:
# Status update: Connected
# Mode: Warp
```

---

### Optional maintenance

* **Disconnect:** `sudo warp-cli disconnect`
* **Restart service:** `sudo systemctl restart warp-svc`
* **Check service:** `sudo systemctl status warp-svc`

---

### Save as a setup file

If you’d like an executable installer, save the above to `install-warp.sh` and make it executable:

```bash
chmod +x install-warp.sh
./install-warp.sh
```

This script performs the exact working sequence you tested on your machine.
