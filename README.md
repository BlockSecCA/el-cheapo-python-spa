# Pyodide State Persistence Demo

[![Status](https://img.shields.io/badge/Status-Ready-brightgreen?style=for-the-badge)](https://github.com/BlockSecCA/el-cheapo-python-spa)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Pyodide](https://img.shields.io/badge/Pyodide-FFD43B?style=for-the-badge&logo=python&logoColor=white)](https://pyodide.org/)
[![SQLite](https://img.shields.io/badge/SQLite-07405E?style=for-the-badge&logo=sqlite&logoColor=white)](https://www.sqlite.org/index.html)
[![Client-Side](https://img.shields.io/badge/Architecture-Client--Side-blue?style=for-the-badge)](https://github.com/BlockSecCA/el-cheapo-python-spa)

A demonstration of running Python applications with persistent state entirely in the browser using Pyodide and WebAssembly.

## What This Demonstrates

This application showcases several key concepts for browser-based Python development:

- **Python in the Browser**: Full Python runtime via Pyodide/WebAssembly
- **Database Operations**: SQLite database operations in browser memory
- **File System Operations**: Virtual file system for Python file I/O
- **State Persistence**: Manual save/load mechanism using browser downloads
- **Scientific Python Stack**: NumPy, Pandas, and other packages available

## How It Works

### Core Architecture

```
Browser Environment
├── Pyodide (Python Runtime)
│   ├── Virtual File System (MEMFS)
│   ├── SQLite Database (app_state.db)
│   ├── JSON State File (app_state.json)
│   └── Python Standard Library
├── JavaScript Interface
└── HTML/CSS UI
```

### State Management

The application maintains state through two mechanisms:

1. **SQLite Database** (`app_state.db`): Stores structured data with timestamps
2. **JSON State File** (`app_state.json`): Tracks counters and execution history

### Persistence Model

Since Pyodide runs in browser memory, state is lost on page refresh. The app provides manual persistence through:

- **Download State**: Exports current state as JSON file to your Downloads folder
- **Upload State**: Restores state from a previously downloaded file
- **Session Management**: Clear current session data

## Features

### Python Environment
- Full CPython 3.12 interpreter
- SQLite3 database support
- NumPy, Pandas scientific computing libraries
- Standard library file operations
- JSON data handling

### State Operations
- **Run Python Code**: Execute Python with database and file operations
- **Check State**: Inspect current files and database contents
- **Download State**: Export complete application state
- **Upload State**: Restore from saved state file
- **Clear Session**: Reset to clean state

## Use Cases

This pattern is particularly valuable for:

### Learning and Experimentation
- Python tutorials that persist student progress
- Data science notebooks with saveable state
- Interactive coding environments
- Educational tools with checkpoint systems

### Lightweight Applications
- Personal data analysis tools
- Simple database applications
- Prototyping and proof-of-concepts
- Offline-capable web apps

### Development Workflows
- Testing Python code without local installation
- Sharing reproducible environments
- Cross-platform Python demos
- Browser-based development tools

## Technical Details

### Dependencies
- **Pyodide**: v0.27.7 (Python 3.12 + scientific stack)
- **Modern Browser**: WebAssembly and ES6+ support required
- **No Server Required**: Runs entirely client-side

### File System
- Virtual file system (MEMFS) - data exists only in browser memory
- Files persist during session but are lost on page refresh
- Manual export/import required for permanent storage

### Security
- All code execution happens in WebAssembly sandbox
- No access to local file system (except downloads/uploads)
- No network access from Python code (browser security)

## Limitations

### Browser Constraints
- **Memory Only**: Virtual file system doesn't persist automatically
- **No Background Processing**: Python execution blocks UI thread
- **Package Limitations**: Only Pyodide-compatible packages available
- **Performance**: 3-5x slower than native Python

### State Management
- **Manual Process**: Save/load requires user interaction
- **No Auto-Sync**: No automatic cloud or local storage
- **Session Isolation**: Each browser tab is independent

## Beyond Client-Side: When Pyodide Visualizations May Not Be Suitable

While Pyodide offers powerful client-side Python execution, there are scenarios where a purely browser-based Python visualization approach (like the ones discussed in the related `pyodide-plotly-shootout` project) may not be suitable, especially when Python is required for data processing:

- **Non-Web-Native GUI Toolkits**: If your Python data processing leads to visualizations exclusively rendered by desktop GUI libraries (e.g., some specialized scientific plotting tools built on PyQt, Tkinter, etc.) that lack web-based counterparts or export options, direct browser display is not feasible.
- **Extreme Performance or Low-Level Browser API Access**: For cutting-edge, highly specialized, or extremely performance-sensitive interactive visualizations that demand direct, low-level manipulation of WebGL/WebGPU contexts or very tight, synchronous loops with browser events, pure JavaScript/TypeScript and WebAssembly (not necessarily Python-in-WebAssembly) might be required for maximum control and minimal overhead.
- **Dependencies on Uncompiled Native C Extensions**: If your Python data processing relies on specific Python packages with critical C extensions that have not been compiled for WebAssembly and included in Pyodide, that part of your Python code cannot run in the browser, preventing a fully client-side visualization workflow.
- **Heavy Server-Side Computation or External Resource Access**: Visualizations that inherently require continuous, heavy server-side Python computation (e.g., very long-running, CPU-intensive calculations that would block the browser's UI thread) or constant interaction with external resources (e.g., massive databases, real-time data streams, proprietary APIs) that cannot be accessed directly from the browser (due to security policies like CORS or performance limitations) will necessitate server-side Python processing, with only the processed results sent to the browser for visualization.

## Getting Started

1. **Open the HTML file** in a modern web browser
2. **Wait for initialization** - Pyodide loads Python and packages
3. **Run the sample code** to create some state
4. **Download State** to save your progress
5. **Refresh and Upload** to test persistence

### Sample Workflow

```python
# Run this code multiple times to build state
import sqlite3
import json
from datetime import datetime

# Creates database and JSON files
# Each run adds timestamped entries
# State accumulates across runs
```

## Future Enhancements

### Automatic Features
- **Auto-save**: Periodic background downloads
- **Smart Persistence**: Browser storage integration
- **Session Recovery**: Restore on accidental refresh

### Advanced Capabilities
- **Package Management**: Dynamic package installation
- **File Upload**: Import CSV/data files for processing
- **Export Options**: Multiple formats (CSV, Excel, etc.)
- **Collaboration**: Share state files between users

## Architecture Benefits

### Cost Efficiency
- **No Server Costs**: Entirely client-side execution
- **No API Calls**: Python runs locally in browser
- **Infinite Scaling**: Each user provides their own compute

### Development Speed
- **Rapid Prototyping**: No deployment pipeline needed
- **Cross-Platform**: Works on any device with browser
- **No Installation**: Users don't need Python installed

### Educational Value
- **Visual**: Students see immediate results
- **Interactive**: Real-time code execution
- **Persistent**: Progress can be saved and shared
- **Accessible**: No technical setup required

## Inspiration & Related Work
Excellent introduction to Python in the browser
- [TestDriven.io Pyodide Tutorial](https://testdriven.io/blog/python-webassembly/) 

---

*This application showcases how modern browsers can run sophisticated Python applications with minimal infrastructure, opening new possibilities for education, prototyping, and lightweight application development.*
