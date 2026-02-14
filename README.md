# 💎 Hacash Diamond GPU Miner

GPU Diamond mining stack for Hacash.

Repository:  
https://github.com/hacashdot/hacash-diamond-gpu-miner

Includes:

- hacashdot-diamond-server  → Diamond Inbox + Web Dashboard (Written in Rust)  
- hacashdot-diamond-miner   → CUDA GPU Diamond Miner (C++ / CUDA)  

------------------------------------------------------------
⚠️ CUDA VERSION & GPU SUPPORT
------------------------------------------------------------

The provided miner binaries are compiled with:

CUDA 12.9

Supported NVIDIA GPU Series:

- RTX 2000 Series (Turing)  
- RTX 3000 Series (Ampere)  
- RTX 4000 Series (Ada Lovelace)  
- RTX 5000 Series (Blackwell)  

Examples:

RTX 2060 / 2070 / 2080  
RTX 3060 / 3070 / 3080 / 3090  
RTX 4090  
RTX 5090  

Requirements:

- NVIDIA Driver compatible with CUDA 12.9  
- CUDA 12.9 runtime installed  

Check your system:

```bash
nvidia-smi
nvcc --version
```

------------------------------------------------------------
ARCHITECTURE
------------------------------------------------------------

GPU Miner  →  Diamond Server (Rust)  →  Hacash Node/API  

• Miner performs X16RS diamond hashing on GPU  
• Rust server manages submissions and validation  
• Web dashboard shows inbox status  
• Server can auto-submit diamonds  

------------------------------------------------------------
SYSTEM REQUIREMENTS
------------------------------------------------------------

- Ubuntu 20.04+ (recommended)  
- NVIDIA GPU (RTX 2000 / 3000 / 4000 / 5000 series)  
- CUDA 12.9  
- Running Hacash node with API enabled  
- Port 9000 accessible (dashboard)  

------------------------------------------------------------
STEP 1 — RUN HACASH NODE
------------------------------------------------------------

Ensure Hacash node API is running.

Example:

```
http://127.0.0.1:8081
```

Verify:

```bash
curl http://127.0.0.1:8081/query/latest
```

------------------------------------------------------------
STEP 2 — INSTALL DIAMOND SERVER (RUST)
------------------------------------------------------------

Download binary:

```bash
wget https://github.com/hacashdot/hacash-diamond-gpu-miner/raw/main/hacashdot-diamond-server
chmod +x hacashdot-diamond-server
```

Environment variables:

```bash
export BACKEND_TOKEN=YOURPASSWORD
export AUTO_PURGE=0
export AUTO_SUBMIT=1
```

Run:

```bash
screen -S hacd-server ./hacashdot-diamond-server
```

------------------------------------------------------------
STEP 3 — ACCESS DASHBOARD
------------------------------------------------------------

Open browser:

```
http://YOUR_NODE_IP:9000
```

Examples:

```
http://127.0.0.1:9000
http://192.168.1.10:9000
http://YOUR_PUBLIC_IP:9000
```

Dashboard shows:

• Pending diamonds  
• Accepted diamonds  
• Failed diamonds  
• Auto-submit status  

------------------------------------------------------------
STEP 4 — INSTALL GPU MINER
------------------------------------------------------------

Download miner:

```bash
wget https://github.com/hacashdot/hacash-diamond-gpu-miner/raw/main/hacashdot-diamond-miner
chmod +x hacashdot-diamond-miner
```

Run miner:

```bash
./hacashdot-diamond-miner --diamond --rpc 127.0.0.1:8081 --gpus 0
```

Multi-GPU example:

```bash
./hacashdot-diamond-miner --diamond --rpc 127.0.0.1:8081 --gpus 0,1,2
```

------------------------------------------------------------
MINER PARAMETERS
------------------------------------------------------------

--diamond             Required flag (diamond mode only)  
--rpc host:port       Hacash node API endpoint  
--gpus                Comma-separated GPU IDs  

------------------------------------------------------------
SECURITY RECOMMENDATIONS
------------------------------------------------------------

If exposing port 9000 publicly:

- Use firewall rules  
- Use reverse proxy with authentication  
- Keep BACKEND_TOKEN secret  

------------------------------------------------------------
COMPONENT SUMMARY
------------------------------------------------------------

hacashdot-diamond-server  
→ Rust-based diamond inbox manager + dashboard  

hacashdot-diamond-miner  
→ CUDA 12.9 GPU miner (RTX 2000 / 3000 / 4000 / 5000 supported)  

------------------------------------------------------------
LICENSE
------------------------------------------------------------

Open source under project license.
