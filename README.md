## 🧠 Event & Scheduling System (Client-Server with GUI)

This project implements a simple distributed system based on a client-server architecture where events, subscriptions, and scheduling algorithms are handled. Clients connect to the server to receive tasks triggered by events, process text files using regex, and manage workload using different scheduling algorithms.

The `src/` directory contains the two main programs:

1. **Server (`server.py`)**
   - Command-line application
   - Manages events and client subscriptions
   - Triggers tasks when events occur
   - Allows configuration of thread count

2. **Client (`client_gui.py`)**
   - Graphical interface (GUI)
   - Connects to the server using an IP and port
   - Subscribe/unsubscribe to events
   - Select scheduling algorithms
   - Receives and processes `.txt` files on trigger
   - Displays process status, metrics, and regex data extraction results in a CSV file

---

## 📁 Project Structure

```text
.
├── README.md           # This file
├── CONTRIBUTING.md     # Guide for contributors
├── TODO.md             # Pending tasks and improvements
├── requirements.txt    # Python dependencies
├── src/                # Source code package
│   ├── __init__.py     
│   ├── server.py       # Server code
│   ├── client_gui.py   # GUI-based client code
│   ├── scheduler.py    # Scheduling algorithms module
│   └── process.py      # Process class module
├── text_files/         # Folder for input .txt files (create manually)
└── output/             # Output folder for CSVs (created by the client)
```

> **Note:** The files `scheduler.py` and `process.py` are proposals to improve modularity, but their functionality may currently be integrated into `client_gui.py` in the initial implementation.

---

## 🚀 Installation

1. Clone this repository:

```bash
git clone https://github.com/ChocoRolis/proyecto-final-SO.git
cd proyecto-final-SO/
```

---

## 🧪 Usage

### 1. Start the Server

Open a terminal and run:

```bash
python3 -m src.server
```

The server will start and wait for incoming client connections. Available commands:
- `add <event>`
- `trigger <event>`
- `set_threads <N>`
- `list`
- `exit`

---

### 2. Prepare `.txt` Files

Place the `.txt` files to be processed in the `text_files/` directory. Make sure they include patterns that will be used for regex-based data extraction.

---

### 3. Start the Client(s)

Open one or more terminals (one per client to simulate) and run:

```bash
python3 -m src.client_gui
```

This will launch the client's graphical interface.

---

### 4. Interact with the Client (GUI)

- Enter the server's IP and port (default: `127.0.0.1:65432`) and click **Connect**.
- Once connected, enter the name of an event (e.g., `data_ready`) and click **Subscribe**.
- Select a scheduling algorithm from the ComboBox.
- *(Optional)* Wait for the server to trigger an event or ask someone managing the server to trigger one you’re subscribed to.
- When tasks are received (after a trigger), click **Start Simulation** to begin processing them according to the selected scheduling algorithm and the number of threads set by the server.
- Use the tabs **Process Table**, **Gantt**, and **CSV Preview** to monitor progress and results.

---

### 5. Stop the Server

In the server terminal, type `exit` and press Enter. This will gracefully shut down the server and notify all connected clients.

---

## 📌 Pending Tasks

Check the [`TODO.md`](TODO.md) file for the list of functionalities yet to be implemented.

---

## 🤝 Contributions

See the [`CONTRIBUTING.md`](CONTRIBUTING.md) file for how to contribute code to this repository.
