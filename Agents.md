# Project: SentinelProxy (Working Title)
# Specification Version: 1.0 (Jan 2026)
# Stack: Go 1.24+, SQLite, Docker

## 1. Core Mandate
A lightweight, open-source AI Gateway and Egress Proxy designed specifically for autonomous AI agents. It sits between the Agent Application and LLM providers (OpenAI, Anthropic, etc.) to provide cost-control, reliability, and observability without requiring code changes in the agent logic.

## 2. System Architecture
- **Ingress:** OpenAI-compatible REST API.
- **Routing:** Path-based routing (e.g., `/v1/chat/completions` -> `api.openai.com`).
- **Data Plane:** Go-based high-performance reverse proxy using `httputil.ReverseProxy`.
- **Storage:** Local SQLite for logs, metadata, and configuration (zero-config startup).

## 3. Key Components
### A. The Gateway Engine (Go)
- **Standard Middleware:** Logging, Recovery, CORS.
- **Circuit Breaker:** Logic to detect 5xx errors from providers and trigger 3 retries or failover to a secondary model (e.g., fallback from GPT-4 to Llama 3).
- **Semantic Cache:** Simple In-memory/SQLite hash-based cache for identical prompts.
- **Streaming Handler:** Must support Server-Sent Events (SSE) for real-time agent responses.

### B. The Guardrail Logic
- **Budget Monitor:** Check `API_KEY` usage against `DAILY_LIMIT` in SQLite before forwarding.
- **Loop Detector:** Track identical requests within a 60-second window to prevent recursive agent loops.
- **Token Parser:** Lightweight regex-based token estimator for cost calculation before provider response arrives.

### C. The Observer (Telemetry)
- **Request Tracing:** Log Every request: Timestamp, AgentID, Model, Latency, Token Count, and Cost.
- **Provider Health:** Background "heartbeat" to check if OpenAI/Anthropic status is "Green."

## 4. API Specification
- Default Base URL: `http://localhost:8080/v1`
- Authenticated via standard `Authorization: Bearer [KEY]`
- Supports `X-Agent-ID` header for granular tracking.