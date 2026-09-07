# EdgeFleet-AI: Distributed Fleet Coordination for Autonomous Mobile Robots (AMRs) in Smart Warehouses

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![FastAPI](https://img.shields.io/badge/Backend-FastAPI%20%7C%20Python%203.12-009688.svg)](https://fastapi.tiangolo.com)
[![WebSocket](https://img.shields.io/badge/RealTime-WebSocket%20100ms-blueviolet.svg)](#real-time-streaming)
[![Edge AI](https://img.shields.io/badge/Architecture-Edge--AI%20Mesh%20%26%20WAN%20Resilience-0ea5e9.svg)](#edge-ai-network-failure-demonstration)

An enterprise-grade warehouse Autonomous Mobile Robot (AMR) fleet coordination platform designed to demonstrate distributed multi-robot task allocation, dynamic A* obstacle avoidance, collision prediction, and **continuous autonomous operation during cloud network failures**.

---

## 🌟 Key Features

### 1. Core Simulation & Robotics Engine (Preserved Foundation)
- **High-Fidelity Physics & Navigation**: Smooth grid navigation with A* path planning, diagonal kinematics, and static shelf obstacle avoidance.
- **Dynamic Collision Avoidance**: Real-time proximity checking with yellow warning envelopes (<70mm) and red hazard rings (<45mm).
- **Battery Management & Smart Docking**: Realistic battery discharge curves and automatic return-to-charger when battery falls below 10%.
- **Multi-Factor FleetAI Allocation**:
  $$\text{Score} = (0.50 \times \text{DistanceScore}) + (0.30 \times \text{BatteryScore}) + (0.20 \times \text{PriorityScore})$$

### 2. Edge AI & Network Failure Demonstration
- **1. Normal Mode**: Cloud-Edge hybrid synchronization (14.2ms latency, 0% packet loss).
- **2. Edge Mode**: Local edge coordinators actively route fleet tasks (3.5ms latency).
- **3. Cloud Failure Mode**: Simulates total wide-area network severance (100% cloud packet loss, 999ms latency). The **Local Edge Decision Engine** seamlessly takes over coordination with **zero robot downtime**.
- **4. Recovery Mode**: Network restored, local telemetry reconciled with cloud database, recovery time benchmarked.

### 3. Enterprise Security & Role-Based Access Control (RBAC)
- **JWT Authentication**: Access and refresh tokens with cryptographic PBKDF2 salt hashing.
- **4 Distinct Roles**:
  1. `Administrator`: Complete system administration, user management, audit logs, warehouse layout.
  2. `Fleet Manager`: Fleet controls, dispatching, AI weights calibration, edge mode switching, report exports.
  3. `Warehouse Operator`: Floor task management, manual robot assignments, alert monitoring.
  4. `Viewer`: Read-only telemetry and monitoring.

### 4. Enterprise SaaS Dashboard & Glassmorphism UI
- **Dual Themes**: Dark Mode (`#0F172A`, `#111827`) & Light Mode with instant persistence.
- **KPI Command Center**: Active Robots, Standby Fleet, Charging AMRs, Battery Hazards, Tasks Completed, Throughput/hr, Network Latency, Edge Mesh Status.
- **High-DPI Warehouse Canvas**: Robot top-down chassis, directional nose pointer, 360° lidar radar sweep cone, battery gauge rings, and glowing A* projected paths.
- **Multi-Format Reports**: Export Daily, Weekly, Monthly, and Utilization reports to **PDF**, **Excel**, and **CSV**.
- **Robotics Intelligence**: Predictive maintenance scoring, vibration RMS analysis, battery depletion forecasting, and spatial congestion heatmap.

---

## 🚀 Quick Start (Windows Desktop)

### Option A: One-Click Launcher
Simply double-click:
```bat
run_enterprise.bat
```
or run in PowerShell:
```powershell
.\run_enterprise.ps1
```
This automatically initializes the database, starts the Uvicorn server, and opens your default browser at `http://127.0.0.1:8000`.

### Option B: Manual Command Line
```powershell
# 1. Initialize database & seed users
python -c "import backend.database; print('Database ready.')"

# 2. Run test suite
python -m unittest tests/test_api.py

# 3. Start server
python -m uvicorn backend.main:app --host 127.0.0.1 --port 8000 --reload
```

---

## 🔑 Pre-Seeded Enterprise Accounts

| Role | Email | Password | Permissions |
| :--- | :--- | :--- | :--- |
| **Administrator** | `admin@edgefleet.ai` | `Admin@123456` | `all`, users, fleet, audit, reports |
| **Fleet Manager** | `manager@edgefleet.ai` | `Manager@123456` | `fleet:read/write`, `tasks:assign`, `edge:control`, `reports:export` |
| **Warehouse Operator** | `operator@edgefleet.ai` | `Operator@123456` | `fleet:read`, `tasks:assign`, `alerts:acknowledge` |
| **Viewer** | `viewer@edgefleet.ai` | `Viewer@123456` | `fleet:read`, `reports:read` |

*(Tip: In the web UI, click the user profile icon in the top right to instantly switch between these accounts with 1 click!)*

---

## 📂 Project Architecture

```
d:/Mechonix/
├── backend/                       # Core Simulation & Enterprise Backend (Python)
│   ├── main.py                   # FastAPI REST API & WebSocket Server
│   ├── simulation.py             # Core AMR Simulation Engine (PRESERVED)
│   ├── robot.py                  # AMR Robot Model & Battery Dynamics (PRESERVED)
│   ├── task.py                   # Warehouse Delivery Mission Model (PRESERVED)
│   ├── warehouse.py              # Warehouse Map & Static Obstacles (PRESERVED)
│   ├── navigation.py             # A* Pathfinder & Collision Avoidance (PRESERVED)
│   ├── ai.py                     # Multi-Factor FleetAI Task Allocation (PRESERVED)
│   ├── database.py               # Enterprise SQLite & PostgreSQL Database Engine
│   ├── auth.py                   # JWT Token Service, PBKDF2 Hashing, RBAC
│   ├── edge_ai.py                # Edge Node Manager & Network Failure Simulator
│   ├── intelligence.py           # Predictive Maintenance, Battery Forecast, Heatmap
│   └── reports.py                # PDF, Excel, and CSV Report Exporters
├── frontend/                      # Production-Ready High-DPI UI
│   ├── index.html                # Modern Glassmorphic Dashboard & Modals
│   ├── style.css                 # Enterprise Robotics Theme & Animations
│   └── js/
│       ├── enterprise_app.js     # High-DPI Canvas Renderer & WebSocket Client
│       └── app.js                # Legacy Reference Controller
├── backend-node/                  # Microservice Node.js + Express + Socket.IO
│   ├── package.json
│   ├── tsconfig.json
│   ├── src/
│   │   ├── server.ts             # Express & Socket.IO Gateway
│   │   └── db/schema.sql         # Full PostgreSQL DDL Schema & Indexes
├── frontend-react/                # Modern React 18 + TypeScript + Tailwind
│   ├── package.json
│   ├── vite.config.ts
│   ├── tailwind.config.js
│   └── src/App.tsx               # Modular React Dashboard
├── tests/
│   └── test_api.py               # Comprehensive Automated Integration Tests
├── docs/                          # Architecture & Reference Documentation
│   ├── API_DOCUMENTATION.md      # OpenAPI / REST Endpoints Reference
│   ├── DATABASE_SCHEMA.md        # Database ER Diagram & Table Reference
│   ├── DEPLOYMENT_GUIDE.md       # Docker & Cloud Deployment Guide
│   └── TESTING_STRATEGY.md       # Quality Assurance & Testing Guide
├── docker-compose.yml             # Orchestration for Postgres, Redis, Core
├── Dockerfile                     # Multi-Stage Production Container
├── run_enterprise.bat             # One-Click Windows Batch Launcher
├── run_enterprise.ps1             # One-Click PowerShell Launcher
└── requirements.txt               # Python Dependencies
```

---

## 🐳 Docker Deployment

To launch the full enterprise stack with PostgreSQL 16 and Redis:
```bash
docker compose up -d --build
```
Access the application at `http://localhost:8000`.

---

## 🧪 Testing & Verification

Run the automated integration test suite:
```powershell
python -m unittest tests/test_api.py
```
Validates:
- System health & backward compatibility
- JWT generation and verification across all 4 roles
- Start / pause / reset simulation state transitions
- Task auto-assignment and multi-factor selection
- Network failure modes (Normal -> Edge -> Cloud Failure -> Recovery)
- Multi-format report export (CSV, Excel, PDF)
- AI predictive maintenance, battery forecasting, and congestion heatmaps

---

## 📄 License
Released under the MIT Enterprise License. &copy; 2026 EdgeFleet Robotics Architecture.
