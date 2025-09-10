# Trading Floor — Agentic Multi-Trader Simulation (with MCP + Accounts Module)

An end-to-end, **agentic trading floor** that runs multiple autonomous trader agents, each with a distinct strategy and toolbelt powered by the **Model Context Protocol (MCP)**.  
It includes:

- A **Trading Floor** orchestrator that schedules and runs traders (Warren, George, Ray, Cathie).
- A live **Gradio dashboard** for portfolio value, holdings, transactions, and logs.
- An **Accounts** system (cash, holdings, transactions, P/L) with an **MCP server**.
- A **Market data** abstraction with Polygon.io support (realtime / delayed / EOD fallback).
- A **Researcher** agent tool for web research + memory via MCP (optional).
- A **CrewAI “Engineering Team”** that generated the Accounts module (design → code → tests → demo UI).
