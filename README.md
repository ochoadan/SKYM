# No Man's Sky Server Modification Framework (SKYM)

![License](https://img.shields.io/badge/license-GNU%20LGPL%202.1-blue)
![Version](https://img.shields.io/badge/version-0.1.0--alpha-orange.svg)
![Status](https://img.shields.io/badge/status-alpha%20development-yellow.svg)

A dedicated server framework for No Man's Sky that replaces the game's native peer-to-peer (P2P) networking with a centralized client-server architecture. Inspired by GMod and FiveM for GTA V, SKYM enables custom multiplayer experiences by introducing server-side control, persistent worlds, and enhanced modding capabilities.

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Technical Architecture](#-technical-architecture)
- [Current Status](#-current-status)
- [Development Roadmap](#-development-roadmap)
- [Project Structure](#-project-structure)
- [Building from Source](#-building-from-source)
- [Contributing](#-contributing)
- [License](#-license)
- [Disclaimer](#%EF%B8%8F-disclaimer)

## 🌌 Project Overview

SKYM creates a custom multiplayer experience for No Man's Sky by implementing a dedicated server framework that intercepts and redirects the game's network calls. By replacing the native peer-to-peer system with a centralized server architecture, this framework enables:

- Custom multiplayer mods and extended functionality
- Enhanced player capacity beyond vanilla limitations
- Server-side scripting for custom gameplay mechanics
- Persistent world states independent of player connections

The project is heavily inspired by FiveM's approach to modding GTA V, focusing on creating an extensible platform for the No Man's Sky modding community.

## 🔧 Technical Architecture

The framework consists of three primary components:

### 1. Server Core (C++)

A high-performance dedicated server written in C++ that:
- Implements the NMS network protocol (reverse-engineered)
- Manages client sessions and authentication
- Handles game state synchronization (world, entities, players)
- Provides robust logging and diagnostics
- Exposes a plugin API for extensions

### 2. Client Hook System

A client-side DLL injection system that:
- Hooks into the No Man's Sky game process
- Redirects network calls to the custom server
- Bypasses official server authentication
- Handles local game state updates
- Manages resource/mod loading

### 3. Scripting & Resource System

A modular scripting engine that:
- Integrates C# scripting (similar to FiveM's CitizenFX)
- Provides a clean API for mod developers
- Enables runtime resource loading
- Facilitates communication between scripts and server/client
- Supports hot-reloading for development

## 🚀 Current Status

SKYM is currently in **early alpha development**. The project is focusing on the core infrastructure and protocol research phase. The following components are being actively developed:

- [x] Project architecture and design
- [ ] Basic server networking layer
- [ ] Client hook system (initial implementation)
- [ ] Protocol reverse-engineering documentation
- [ ] Connection handshake implementation

## 📈 Development Roadmap

### Phase 1: Foundation (Current)
- [x] Define technical architecture
- [ ] Implement minimal server with client connection handling
- [ ] Create client hook system for network redirection
- [ ] Establish basic server-client communication
- [ ] Implement authentication bypass
- [ ] Develop heartbeat system for connection management

### Phase 2: Protocol Research
- [ ] Reverse-engineer NMS network protocol
- [ ] Document message formats and structures
- [ ] Implement protocol handlers on server and client
- [ ] Create testing tools for protocol validation

### Phase 3: Core Functionality
- [ ] Implement player position synchronization
- [ ] Develop entity state management
- [ ] Create world state synchronization
- [ ] Design resource loading system
- [ ] Integrate C# scripting engine

### Phase 4: Extended Features
- [ ] Implement inventory and player state synchronization
- [ ] Add support for custom gameplay mechanics
- [ ] Develop admin tools and monitoring interface
- [ ] Create persistence layer for world state
- [ ] Build plugin system for server extensions

### Phase 5: Optimization & Documentation
- [ ] Performance optimization
- [ ] Security hardening
- [ ] Comprehensive API documentation
- [ ] Example mods and scripting guides
- [ ] Community resource development

## 📁 Project Structure

```
SKYM/
├── server/                           # Server Component
│   ├── src/
│   │   ├── core/                     # Core server functionality
│   │   │   ├── server.h/cpp          # Main server implementation
│   │   │   ├── client_manager.h/cpp  # Client session management
│   │   │   └── config.h/cpp          # Configuration handling
│   │   ├── network/                  # Network layer
│   │   │   ├── protocol.h/cpp        # Protocol implementation
│   │   │   ├── socket.h/cpp          # Network socket abstraction
│   │   │   └── packet_handler.h/cpp  # Packet processing
│   │   ├── game/                     # Game state management
│   │   │   ├── entity.h/cpp          # Entity system
│   │   │   ├── world.h/cpp           # World state
│   │   │   └── player.h/cpp          # Player data
│   │   ├── scripting/                # Scripting engine
│   │   │   ├── script_engine.h/cpp   # Script runtime
│   │   │   ├── api.h/cpp             # Scripting API
│   │   │   └── resource_manager.h/cpp # Resource loading
│   │   └── utils/                    # Utilities
│   │       ├── logger.h/cpp          # Logging system
│   │       └── helpers.h/cpp         # Helper functions
│   ├── tests/                        # Server tests
│   └── CMakeLists.txt                # Build configuration
│
├── client/                           # Client Hook Component
│   ├── src/
│   │   ├── core/                     # Core client functionality
│   │   │   ├── dllmain.cpp           # DLL entry point
│   │   │   ├── hook_manager.h/cpp    # Hook management
│   │   │   └── config.h/cpp          # Client configuration
│   │   ├── hooks/                    # Game hooks
│   │   │   ├── network_hooks.h/cpp   # Network function hooks
│   │   │   └── game_hooks.h/cpp      # Game function hooks
│   │   ├── network/                  # Network layer
│   │   │   ├── server_connection.h/cpp # Server connection
│   │   │   └── packet_handler.h/cpp  # Packet handling
│   │   ├── scripting/                # Script integration
│   │   │   ├── resource_loader.h/cpp # Resource loading
│   │   │   └── script_bindings.h/cpp # Script bindings
│   │   └── utils/                    # Utilities
│   │       ├── logger.h/cpp          # Logging system
│   │       └── pattern_scan.h/cpp    # Memory pattern scanning
│   ├── tests/                        # Client tests
│   └── CMakeLists.txt                # Build configuration
│
├── common/                           # Shared Code
│   ├── include/
│   │   ├── protocol/                 # Protocol definitions
│   │   │   ├── messages.h            # Message structures
│   │   │   ├── types.h               # Data types
│   │   │   └── constants.h           # Protocol constants
│   │   ├── scripting/                # Shared scripting
│   │   │   ├── api_definitions.h     # API definitions
│   │   │   └── resource_defs.h       # Resource definitions
│   │   └── utils/                    # Shared utilities
│   │       ├── types.h               # Common type definitions
│   │       └── math.h                # Math utilities
│   └── CMakeLists.txt                # Build configuration
│
├── scripting/                        # Scripting Engine
│   ├── src/
│   │   ├── runtime.h/cpp             # C# runtime implementation
│   │   ├── bindings.h/cpp            # Native bindings
│   │   └── api.h/cpp                 # API implementation
│   ├── api/                          # Public API for scripts
│   │   ├── Server.cs                 # Server API
│   │   ├── Client.cs                 # Client API
│   │   ├── Entity.cs                 # Entity API
│   │   └── World.cs                  # World API
│   ├── examples/                     # Example scripts
│   └── CMakeLists.txt                # Build configuration
│
├── tools/                            # Development Tools
│   ├── protocol_analyzer/            # Protocol analysis tools
│   ├── packet_inspector/             # Packet inspection utility
│   └── resource_compiler/            # Resource compilation tools
│
├── thirdparty/                       # Third-party Dependencies
│   ├── asio/                         # ASIO networking library
│   ├── minhook/                      # MinHook for function hooking
│   ├── spdlog/                       # Logging library
│   └── mono/                         # Mono for C# scripting
│
├── resources/                        # Default Resources
│   ├── base/                         # Base game resources
│   └── examples/                     # Example mods
│
├── docs/                             # Documentation
│   ├── protocol.md                   # Protocol documentation
│   ├── scripting_api.md              # Scripting API docs
│   └── architecture.md               # Architecture overview
│
├── scripts/                          # Build & Utility Scripts
│   ├── build.bat                     # Windows build script
│   ├── build.sh                      # Linux build script
│   └── install.bat                   # Client installation script
│
├── .github/                          # GitHub Configuration
│   └── workflows/                    # CI/CD workflows
│
├── CMakeLists.txt                    # Root build configuration
├── README.md                         # Project overview
└── LICENSE                           # GNU LGPL License
```
### Architecture Diagram

```
┌────────────────────────────┐                  ┌────────────────────────────┐
│ Client Side                │                  │ Server Side                │
│ ┌────────────────────────┐ │                  │ ┌────────────────────────┐ │
│ │    No Man's Sky Game   │ │                  │ │ Dedicated Server Core  │ │
│ └───────────┬────────────┘ │                  │ └────────────┬───────────┘ │
│             │              │                  │              │             │
│ ┌───────────▼────────────┐ │                  │ ┌────────────▼───────────┐ │
│ │    Client Hook DLL     │ │                  │ │  Network Layer         │ │
│ └───────────┬────────────┘ │                  │ └────────────┬───────────┘ │
│             │              │                  │              │             │
│ ┌───────────▼────────────┐ │                  │ ┌────────────▼───────────┐ │
│ │  Network Redirection   │ │                  │ │ Session Management     │ │
│ └───────────┬────────────┘ │◄─── TCP/UDP ────►│ └────────────┬───────────┘ │
│             │              │                  │              │             │
│ ┌───────────▼────────────┐ │                  │ ┌────────────▼───────────┐ │
│ │  Resource Manager      │ │                  │ │ Entity/World State     │ │
│ └───────────┬────────────┘ │                  │ └────────────┬───────────┘ │
│             │              │                  │              │             │
│ ┌───────────▼────────────┐ │                  │ ┌────────────▼───────────┐ │
│ │  C# Script Runtime     │ │◄─── Events ─────►│ │ C# Script Engine       │ │
│ └────────────────────────┘ │                  │ └────────────────────────┘ │
└────────────────────────────┘                  └────────────────────────────┘
```
## 🔨 Building from Source

### Prerequisites

- Visual Studio 2019+ (Windows) or GCC 9+ (Linux)
- CMake 3.14+
- Python 3.8+ (for build scripts)
- .NET SDK 6.0+ (for scripting engine)
- Git

### Server Build

```bash
# Clone the repository with submodules
git clone --recursive https://github.com/ochoadan/SKYM.git
cd SKYM

# Create build directory
mkdir build
cd build

# Configure and build
cmake ..
cmake --build . --config Release
```

### Client Build

```bash
# From the build directory
cmake .. -DBUILD_CLIENT=ON
cmake --build . --config Release
```

## 👥 Contributing

All contributions are welcome and encouraged! The project is in early development and needs support in various areas.

### Contribution Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

### Key Contribution Areas

- Protocol research and reverse engineering
- Core network functionality
- Client hook implementation
- C# scripting engine integration
- Documentation and examples
- Testing and bug reports

## 📄 License

This project is licensed under the GNU LGPL 2.1 License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Disclaimer

This project is not affiliated with, endorsed by, or connected to *Hello Games* or *No Man's Sky*. This is an unofficial, fan-made project. Use at your own risk.