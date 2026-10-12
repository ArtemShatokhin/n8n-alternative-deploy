# Open source n8n alternative FAQ

## Is Kortix open source?

Yes. Kortix is the open-source AI Operating System. The code is public: read it, fork it and audit it at [Kortix on GitHub](https://github.com/kortix-ai/suna).

## Is n8n open source?

n8n describes itself as fair-code, distributed source-available under the Sustainable Use License and the n8n Enterprise License ([n8n-io/n8n](https://github.com/n8n-io/n8n), checked October 2026). It is not offered under an OSI-approved open-source license.

## What is the difference between Kortix and n8n?

n8n runs the diagram you draw: the same nodes fire in the same order on every execution. Kortix hands an open-ended job to an agent that plans its own steps on its own isolated cloud computer, calls your connectors as tools, and finishes by opening a change request a person approves.

## Can I self-host Kortix for free?

Yes. Self-host is free, and the stack is one Docker Compose project. You pay only for the compute you point it at and the model keys you bring.

## Which models can Kortix run?

Any model provider with your own keys, or the ChatGPT plan you already pay for. You pick the model per agent, per session or per message.

## Where does Kortix run?

Kortix Cloud, your own VPC, or your own on-prem network. Self-hosted instances run the control plane on your hardware, and agent sessions run on a separate sandbox provider.

## Can a workflow still run on a schedule?

Yes. A trigger starts a session on a cron schedule or a signed webhook, with nobody present, and the agent opens a change request with the finished work.

## How does the work get approved?

Session work reaches `main` through a change request you read as a diff before anything merges. Merge is default-deny for agents, and approval gates can hold any tool call until a person approves it.
