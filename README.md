# 🛡️ SentinelProxy: The Safety Belt for AI Agents

![Version](https://img.shields.io/badge/version-0.1.0--alpha-orange)

## The Problem

In 2026, agents are autonomous. If your agent hits a recursive loop while you're asleep, you could wake up to a $2,000 bill. If an LLM provider has a minor outage, your agent crashes. If your agent leaks customer data into a prompt, you're liable.

## The Solution

SentinelProxy is a one-binary, zero-config egress proxy that gives you total control over your agents' external interactions. It's open-source, runs locally, and acts as a "kill switch" and "black box recorder" for your AI stack.

## Why It's Better

- **Drop-in Replacement**: Just change your `BASE_URL` in your OpenAI or LangChain config. No new libraries to learn.

- **Budget Guardrails**: Set a hard $5/day limit. If the agent goes over, the proxy cuts the connection.

- **Infinite Loop Protection**: Automatically detects and kills agents that get stuck asking the same thing.

- **Privacy First**: All logs stay in a local SQLite database on your machine. We never see your data.

## The Roadmap

- **v0.1 (MVP)**: Go proxy + OpenAI routing + SQLite cost logging.

- **v0.2 (Reliability)**: Automatic failover (If GPT-4 is down, use Claude).

- **v0.3 (Observability)**: Simple local dashboard to view "Reasoning Traces."

- **v1.0 (Cloud)**: Optional managed version for teams with multi-agent coordination.

- CLI header: 
🛡️  SentinelProxy v0.1.0-alpha
⚠️  Alpha software: Always maintain provider-level spending limits

## License
   Apache 2.0 - See LICENSE file for details.