# 🧩 NUC Video Redundancy Mesh (C++ PoC)

## Objective
Simulate a **fault-tolerant, storage-efficient video redundancy mesh** where multiple NUC-like nodes record camera feeds, encode them into resilient shards, and exchange them with peers to ensure data recovery on failure.

## Architecture Overview

### Core Services
- **Peer Discovery:** Detects live nodes on LAN.  
- **Video Capture:** Reads frames from pre-recorded or live video.  
- **Segmentation:** Groups frames into short micro-segments.  
- **RS Encoding / Sharding:** Splits segments into data + parity shards.  
- **Shard Distribution:** Sends shards to peers reliably.  
- **Metadata Service:** Tracks shard location and status.  
- **Monitoring / Recovery:** Detects failures and reconstructs lost shards.  
- **Backend Sync:** Uploads confirmed segments and purges local storage.

### Folder Structure
```
nuc-video-mesh/
├── CMakeLists.txt
├── src/
│ ├── main.cpp
│ ├── utils/
│ │ └── logger.cpp / logger.hpp
│ ├── services/
│ │ ├── peer_discovery.cpp / .hpp
│ │ ├── video_capture.cpp / .hpp
│ │ ├── segmentation.cpp / .hpp
│ │ ├── rs_encoding.cpp / .hpp
│ │ ├── shard_distribution.cpp / .hpp
│ │ ├── metadata_service.cpp / .hpp
│ │ ├── monitoring_recovery.cpp / .hpp
│ │ └── backend_sync.cpp / .hpp
└── build/ (auto-generated)
```



### Build & Run
```bash
mkdir build && cd build
cmake ..
cmake --build .
./nuc_video_mesh --node-id 1 --port 5001
./nuc_video_mesh --node-id 2 --port 5002
```
###  Key Libraries & Tools

- C++17
- Boost.Asio / ZeroMQ → Networking & shard distribution
- SQLite → Metadata persistence
- FFmpeg / OpenCV → Video capture and segmentation
- Jerasure / libfec → RS encoding for redundancy
- CMake → Build and dependency management

### Testing Scenarios

- Single node recording and local shard storage
- Multi-node shard exchange simulation
- Node failure recovery
- Backend upload and purge workflow