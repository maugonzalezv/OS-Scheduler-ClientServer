# 🔥 OS Event & Scheduling System – Detailed Feature Overview

## 📄 Overview

This is a complex distributed system combining operating-system concepts, file processing, and scheduling algorithm simulations. It features a client–server architecture demonstrating real concurrency on the server and interactive scheduling visualization on the client.

---

## 🏛️ System Architecture

### 1. Central Server (`server.py`)

Acts as the system’s core, handling multiple responsibilities:

#### 🌐 Connectivity Management

* **TCP Socket** listening on `127.0.0.1:65432` for client connections
* **Multi-Client Handling**: Each client runs on its own thread
* **Unique Client IDs**: Assigned upon connection
* **Fault Tolerance**: Robust handling of unexpected disconnects

#### 🔔 Event System

* **Event Subscription**: Clients subscribe to specific events
* **FIFO Queues**: Each event maintains its subscriber list
* **Manual Triggers**: Events activated via server console
* **Fair Distribution**: Files evenly distributed among clients

#### 🗂️ File Processing

* **Configurable Concurrency**: Clients choose:

  * **Mode**: `threads` or `forks`
  * **Workers**: Number of concurrent workers
* **ThreadPoolExecutor / ProcessPoolExecutor** for real concurrency
* **Detailed Logging** in `server_processing.log`
* **PID Monitoring** of worker threads/processes

#### 🕵️ Regex-Based Data Extraction

* **Text Analysis** of `.txt` files using regex
* **Pattern Extraction**:

  * **Names** (e.g. "John Smith", "Anna Karlsson")
  * **Dates** (textual & numeric formats)
  * **Places** from a predefined multilingual city list
  * **Word Counts** for statistical insights
* **Error Handling** for corrupt files

---

### 2. GUI Client (`client_gui.py`)

A full-featured Tkinter application with advanced UI:

#### 🎨 User Interface

* **Custom Theme**: Professional, consistent color scheme
* **Responsive Layout** with auto-scrolling
* **Tabbed Navigation** for clear feature organization
* **Input Validation** for robust data entry

#### 🔌 Connection Management

* **Configurable IP & Port**
* **Connection Status Indicators**
* **Auto-Reconnect** on disconnect
* **Configurable Timeouts**

#### ⚙️ Client Configuration

* **Processing Mode**: Toggle threads vs. processes
* **Worker Count**: Slider to adjust concurrency
* **Real-Time Updates**: Settings sent immediately to server

#### 🎯 Event Subscription

* **Multi-Event Subscriptions** per client
* **Visual List** of active subscriptions
* **Notifications** when events trigger

#### 📊 Scheduling Simulation

* **Algorithms Supported**:

  * **FCFS (First-Come, First-Served)**
  * **SJF (Shortest Job First)**
  * **SRTF (Shortest Remaining Time First)**
  * **Round Robin** (configurable quantum)
  * **HRRN (Highest Response Ratio Next)**
  * **Non-Preemptive Priority**
* **Parameter Inputs**:

  * Arrival Time
  * Burst Time
  * Priority
  * Quantum

#### 🎥 Visualization

* **Process Table** showing each process’s state
* **Animated Gantt Chart** of execution timeline
* **Performance Metrics**:

  * Turnaround Time
  * Waiting Time
  * Response Ratio calculations & averages

---

### 3. Scheduling Engine (`scheduler.py`)

Educational implementation of scheduling algorithms:

#### ⚙️ Abstract Base Class

* **Common Interface**: Standard `schedule()` method
* **Parametrized** for ready queues, current time, running processes
* **Supports** both preemptive & non-preemptive modes

#### 🔄 Specific Algorithms

* **FCFS**: Basic FIFO implementation
* **SJF**: Shortest burst time selection
* **SRTF**: Preemptive shortest remaining time
* **Round Robin**: Quantum-based preemption
* **HRRN**: Dynamic response ratio calculation
* **Priority**: Numeric-based selection

---

### 4. Data Model (`process.py`)

Defines the process representation:

#### 📝 Attributes

* **PID & Name**
* **Times**: Arrival, Burst, Start, Completion
* **State**: New, Ready, Running, Terminated
* **Metrics**: Waiting, Turnaround, Response Ratio
* **Metadata**: Priority, Remaining Burst Time

#### 🔧 Methods

* **`__str__` & `__repr__`** for clear text output
* **Automatic Metric Updates**
* **Documented Formulas**

---

### 5. Regex Extractor (`extractor_regex.py`)

Regex-driven text processor:

#### 🔍 Extraction Patterns

* **Proper Names** via regex
* **Dates** in multiple locales & formats
* **Geographical Locations** from curated list
* **Statistical Analysis**: Word & character counts

#### 🛡️ Robustness

* **Error Recovery** for damaged files
* **UTF-8 Support** with fallback handlers
* **Deduplication** & alphabetical sorting

---

## 🚀 Workflow

1. **Initialize**:

   * Server searches `text_files/` for `.txt` files
   * Client connects & authenticates
   * Client sends concurrency settings
   * Client subscribes to events

2. **Server Processing**:

   * Admin triggers an event
   * Files distributed evenly among clients
   * Concurrent processing & regex extraction
   * Logs consolidated & sent back

3. **Client Simulation**:

   * User selects files & algorithm
   * Simulation runs step-by-step
   * Visualizations & metrics update in real time

4. **Analysis**:

   * Process table & Gantt chart
   * Performance statistics displayed
   * Option to export results to CSV

---

## ✅ Key Use Cases

### 🔎 Historical Document Analysis

* Extract names, dates, & places from archival texts
* Parallel processing for speed

### 🎓 OS Education Tool

* Interactive teaching of scheduling algorithms
* Performance comparison between methods

### 📈 Performance Benchmarking

* Measure threading vs. forking via throughput & latency

---

## 🔧 Advanced Features

* **Concurrency Modes**: Threads vs. Processes
* **Fault Handling**: Granular exceptions & auto-recovery
* **Optimizations**: Lazy loading, caching, batch processing
* **Scalability**: Multi-client support & load balancing

---

## 🔒 Security Considerations

* **Input Sanitization** & validation
* **Path traversal prevention** & file size limits
* **Network safeguards**: Timeouts, buffer overflow checks

---

*This document highlights a fully detailed, production-style OS scheduling and event-processing system—perfect for education, research, and demonstrative purposes!*
