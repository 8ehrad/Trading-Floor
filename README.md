# Trading Floor and AI Engineering Team

This repository houses two main components: an AI Agent-based Code Generation System and a Trading Simulation Platform.

## 1. AI Agent-based Code Generation System (`engineering_team/`)

This system utilizes `crewai` to automate the generation of Python code based on high-level requirements. It simulates an engineering team workflow, producing detailed design documents, backend modules, Gradio UIs, and unit tests.

### Core Components:
- **`main.py`**: Orchestrates the `EngineeringTeam` crew, defines project requirements, and initiates the code generation process.
- **`crew.py`**: Defines the structure of the engineering team, including roles for the Engineering Lead, Backend Engineer, Frontend Engineer, and Test Engineer. It also outlines their respective tasks (design, coding, frontend development, and testing).
- **`config/agents.yaml`**: Configures the roles, goals, and backstories for each AI agent in the engineering team.
- **`config/tasks.yaml`**: Details the specific tasks assigned to each agent, including descriptions, expected outputs, and output file paths.
- **`tools/custom_tool.py`**: A placeholder for custom tools that can be integrated into the agent workflows.
- **`example_output_*/`**: Directories containing examples of generated code and design documents from previous runs of the system.

### How it Works:
The system takes a set of requirements for a software module. The Engineering Lead agent then creates a detailed design. The Backend Engineer implements the design, the Frontend Engineer builds a Gradio UI for it, and the Test Engineer writes unit tests. The outputs are organized into specific directories.

## 2. Trading Simulation Platform (`trading_floor/`)

This platform provides a realistic environment for simulating trading activities, allowing AI agents to interact with a market, manage accounts, and execute trades.

### Core Components:
- **`trading_floor.py`**: The main entry point for the trading simulation. It initializes and runs multiple `Trader` agents, which make periodic trading decisions based on market conditions.
- **`accounts.py`**: Manages individual trading accounts, handling deposits, withdrawals, buying/selling shares, tracking holdings, calculating portfolio value, and logging transactions.
- **`market.py`**: Interfaces with the Polygon API to fetch real-time or end-of-day stock prices. It also includes logic to check market open/close status.
- **`accounts_server.py`**: Exposes account management functionalities (e.g., `get_balance`, `buy_shares`, `sell_shares`) as `FastMCP` microservices, allowing other components or external systems to interact with trading accounts.
- **`market_server.py`**: Exposes a `lookup_share_price` tool via `FastMCP`, enabling services to query stock prices.
- **`traders.py`**: Defines the `Trader` class, which encapsulates the AI agent's trading strategies and decision-making logic.
- **`database.py` (inferred)**: Handles data persistence for trading accounts, market data, and transaction logs.
- **`push_server.py` (inferred)**: Likely a server component responsible for pushing real-time updates to connected clients or UIs.
- **`reset.py`**: A script for resetting the trading environment, such as clearing account data or market history.
- **`templates.py`**: May contain templates for generating reports, UI elements, or other structured outputs.
- **`tracers.py`**: Provides logging and tracing capabilities to monitor agent activities and system events.
- **`util.py`**: A collection of utility functions used across the trading platform.
- **`app.py`**: A user interface for the trading floor, potentially built with Gradio (inferred from `engineering_team` outputs).
- **`mcp_params.py`**: Configuration parameters for the `FastMCP` microservices.
- **`memory/memory.txt`**: Used for persistent memory or state management for trading agents.

## Setup and Installation

### Prerequisites

- Python 3.12 or higher
- `uv` for dependency management

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-repo/Trading-Floor.git
    cd Trading-Floor
    ```

2.  **Install dependencies using `uv`:**
    ```bash
    uv pip install -r requirements.txt
    ```
    or
    ```bash
    uv pip install -e .
    ```

3.  **Environment Variables:**
    Create a `.env` file in the root directory and add the following (at a minimum):
    ```
    POLYGON_API_KEY="YOUR_POLYGON_API_KEY"
    POLYGON_PLAN="paid" # or "free"
    RUN_EVERY_N_MINUTES="60"
    RUN_EVEN_WHEN_MARKET_IS_CLOSED="false"
    USE_MANY_MODELS="false"
    ```

### Running the Systems

#### AI Agent-based Code Generation

To run the AI engineering team to generate code for new requirements:

```bash
python -m engineering_team.src.engineering_team.main
```

#### Trading Simulation Platform

To start the trading simulation with AI traders:

```bash
python -m trading_floor.trading_floor
```

To run the MCP servers (if needed independently):

```bash
python -m trading_floor.accounts_server
python -m trading_floor.market_server
```

## Project Structure

```
.
├── engineering_team/
│   ├── example_output_4o/
│   ├── example_output_mini/
│   ├── example_output_new/
│   ├── knowledge/
│   ├── pyproject.toml
│   ├── src/
│   │   └── engineering_team/
│   │       ├── config/
│   │       ├── crew.py
│   │       ├── main.py
│   │       └── tools/
│   └── uv.lock
├── pyproject.toml
├── requirements.txt
├── trading_floor/
│   ├── accounts_client.py
│   ├── accounts_server.py
│   ├── accounts.py
│   ├── app.py
│   ├── database.py
│   ├── market_server.py
│   ├── market.py
│   ├── mcp_params.py
│   ├── memory/
│   ├── push_server.py
│   ├── reset.py
│   ├── templates.py
│   ├── tracers.py
│   ├── traders.py
│   ├── trading_floor.py
│   └── util.py
└── uv.lock
```
