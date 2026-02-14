# hacashdot-diamond

Official GPU Diamond Mining stack for Hacash.

Includes:

- hacashdot-diamond-server   (Diamond Inbox + Dashboard)
- hacashdot-diamond-miner    (CUDA GPU Diamond Miner)

------------------------------------------------------------
ARCHITECTURE
------------------------------------------------------------

GPU Miner  →  Diamond Server (Inbox)  →  Hacash Node/API

- Miner finds diamonds using GPU
- Server receives, verifies, and optionally auto-submits
- Dashboard allows monitoring via web UI

------------------------------------------------------------
REQUIREMENTS
------------------------------------------------------------

- Linux (Ubuntu recommended)
- CUDA-capable GPU
- Running Hacash node with API enabled
- Port 9000 open (for dashboard access)

------------------------------------------------------------
1) START DIAMOND SERVER
------------------------------------------------------------

Run on SAME machine where Hacash node/API is installed.

export BACKEND_TOKEN=YOURPASSWORD
export AUTO_PURGE=0
export AUTO_SUBMIT=1

screen -S hacd-server ./hacashdot-diamond-server

Detach screen:
Ctrl + A + D

Reattach:
screen -r hacd-server

------------------------------------------------------------
2) START GPU DIAMOND MINER
------------------------------------------------------------

./hacashdot-diamond-miner --diamond --rpc 127.0.0.1:8081 --gpus 0

Multi-GPU example:

./hacashdot-diamond-miner --diamond --rpc 127.0.0.1:8081 --gpus 0,1,2

Parameters:

--diamond             Required flag (diamond mode only)
--rpc host:port       Hacash node API endpoint
--gpus                Comma separated GPU IDs

------------------------------------------------------------
3) ACCESS DIAMOND INBOX DASHBOARD
------------------------------------------------------------

Open browser:

http://YOUR_NODE_IP:9000

Examples:

http://127.0.0.1:9000
http://192.168.1.10:9000
http://YOUR_PUBLIC_IP:9000

Dashboard Features:

- View mined diamonds
- See pending submissions
- Monitor accepted diamonds
- View failed submissions
- Auto purge control (if enabled)

------------------------------------------------------------
ENVIRONMENT VARIABLES
------------------------------------------------------------

BACKEND_TOKEN=YOURPASSWORD    Protects submission endpoint
AUTO_SUBMIT=1                 Auto-submit valid diamonds
AUTO_PURGE=1                  Auto-clean old inbox entries

------------------------------------------------------------
SECURITY NOTES
------------------------------------------------------------

If exposing port 9000 publicly:

- Use firewall rules
- Use reverse proxy with authentication
- Keep BACKEND_TOKEN secret

------------------------------------------------------------
PROJECT STRUCTURE
------------------------------------------------------------

hacashdot-diamond-server   → Inbox + Dashboard
hacashdot-diamond-miner    → CUDA Diamond GPU miner

------------------------------------------------------------
