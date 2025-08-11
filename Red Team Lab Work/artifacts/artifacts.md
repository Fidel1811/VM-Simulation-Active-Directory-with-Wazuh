# Day 1 Notes — Red Team

**Date:** 2025-08-11  
**Duration:** ~3 hours  

## Activities
1. **Goal:** Run OWASP Juice Shop on host (Docker) and confirm access from Kali VM.
2. Attempted to start Juice Shop container:
   ```bash
   docker run -d --name juice-shop -p 3000:3000 bkimminich/juice-shop
    ```

Encountered Cannot connect to the Docker daemon → determined Docker not installed.

3. Checked Docker service:

```bash
sudo systemctl start docker
```

4. Result: Unit docker.service not found → confirmed Docker installation needed.

   Investigated DNS resolution issue on Kali:

   Found /etc/hosts mapping domains to 127.0.0.1.

   Removed incorrect entries to restore proper resolution.

Findings:

Docker is not currently installed/configured on host; blocking container deployment.

Kali VM’s DNS problem was due to hosts file override, not upstream DNS server.

No recon (nmap/curl) performed yet as service was unavailable.

Next Steps:

Install and start Docker on host.

Run Juice Shop container in detached mode with persistent logs.

From Kali, perform safe recon:

Browser check (http://<host-ip>:3000)

Service discovery (nmap -sV -p 3000 <host-ip>)

Headers check (curl -I http://<host-ip>:3000)

Capture topology diagram, screenshots, and logs for artifacts.

```bash
Once Docker is working, you can just add the recon and screenshot details to this same file for completeness.  

Do you also want me to prepare the **Day 2 blue-team notes template** now so you can just fill it in tomorrow? That way your documentation stays consistent across days.
```


