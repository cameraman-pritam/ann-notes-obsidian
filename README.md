***
## 📓 The Obsidian Knowledge Vault

This repository contains an Obsidian vault designed to document the _why_ and _how_ of the entire pipeline, not just the math. It acts as a deep-dive notebook covering:

1. **The Math Behind ANN**: Step-by-step breakdowns of the dimensional contract, dot products, partial derivatives (Chain Rule), and the Exploding Gradient problem.
    
2. **C++ Systems & Architecture**: Memory allocation, `std::vector` contiguous memory guarantees, and the mechanics of the Mersenne Twister (`mt19937`) for symmetry breaking.
    
3. **Data Parsing & Binary I/O**: How the generalized CSV parser works line-by-line, and the exact byte-level structure of the `.bin` model files.
    
4. **Deployment Playbooks**: Guides on compiling the C++ engine to WebAssembly via Emscripten for React frontend integration, or wrapping it in a native REST API (e.g., `crowcpp`).
    

_To view the documentation, simply open the `Obsidian_Vault` folder as a vault in the [Obsidian](https://obsidian.md/) app._

## 🚀 Getting Started

### Prerequisites

- **C++ Compiler**: GCC or Clang (C++17 or higher)
    
- **Build Tools**: CMake & Make / Ninja
    
- **Package Manager**: Conan 2.x (Optional, for extending the project)
    
- **WebAssembly Toolchain**: Emscripten (If compiling for the web)
    

### 1. Native Build (Linux / Arch Linux)

Configure and compile the project as a standalone native binary:

Bash

```
mkdir build && cd build
cmake ..
cmake --build .
./cpp_ann_engine
```

### 2. WebAssembly Build (Emscripten)

Compile the C++ math engine into a `.wasm` file to run directly in a browser (e.g., alongside a React frontend) with zero server latency:

Bash

```
mkdir build_wasm && cd build_wasm
emcmake cmake ..
emmake make
```

_This will generate `.wasm` and `.js` glue code for client-side ML inference._

## 🌐 Deployment Strategies

This engine is architected to be deployed in two primary ways:

1. **The Edge / Frontend (WebAssembly)**: The recommended approach. The C++ engine is compiled to Wasm. When a user draws a digit on an HTML canvas, the React app passes the raw pixel array directly to the Wasm module. The prediction happens entirely on the user's local CPU.
    
2. **Serverless API (Backend)**: The C++ code is wrapped in an HTTP library (like `cpp-httplib` or `crowcpp`) and hosted as a Dockerized microservice on platforms like Render or Fly.io.