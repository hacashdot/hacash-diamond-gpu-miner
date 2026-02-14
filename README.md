# hacash-diamond-gpu-miner
Hacash Diamond GPU Minter

GPU-accelerated Hacash Diamond mining system with inbox server for automatic submission.

------------------------------------------------------------
REQUIREMENTS
------------------------------------------------------------
- Linux (Ubuntu recommended)
- CUDA-capable GPU
- Hacash node + API running locally
- screen installed

------------------------------------------------------------
ARCHITECTURE
------------------------------------------------------------
dminer (GPU)  →  dmserver (Inbox Server)  →  Hacash Node/API

- dminer finds diamonds using GPU
- dmserver receives, verifies, and optionally auto-submits
- Hacash node validates and adds to blockchain

------------------------------------------------------------
STEP 1: INSTALL & RUN DIAMOND INBOX SERVER
------------------------------------------------------------
Install on the SAME machine where the Hacash node/API is running.

Set environment variables:

export BACKEND_TOKEN=YOURPASSWORD
export AUTO_PURGE=0
export AUTO_SUBMIT=1

Run server inside screen:

screen -S dmserver ./dmserver

Detach:
Ctrl + A + D

Reattach:
screen -r dmserver

------------------------------------------------------------
STEP 2: RUN GPU DIAMOND MINER
------------------------------------------------------------

./dminer --diamond --rpc-hostport 127.0.0.1:8081 --gpus 0

OPTIONS:
--diamond              Enable diamond mining mode
--rpc-hostport         Hacash node API address
--gpus                 GPU index (comma separated for multiple GPUs)

Example (multi-GPU):

./dminer --diamond --rpc-hostport 127.0.0.1:8081 --gpus 0,1,2

------------------------------------------------------------
AUTO SUBMIT CONTROL
------------------------------------------------------------
AUTO_SUBMIT=1   Automatically submit valid diamonds
AUTO_SUBMIT=0   Manual submission mode
AUTO_PURGE=1    Auto clear old inbox entries

------------------------------------------------------------
NOTES
------------------------------------------------------------
- Ensure firewall allows local RPC access
- Keep backend token secure
- Mining difficulty increases over time
- GPU performance directly impacts mint rate
