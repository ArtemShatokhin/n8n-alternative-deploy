# Kortix vs n8n

Kortix and n8n both automate work, and they are built around different units: n8n runs a fixed flowchart of nodes, and Kortix hands an open-ended job to an agent that plans its own steps. The choice is less about features than about whether the steps are known before the work starts.

## The head-to-head

| Dimension | Kortix | n8n |
| --- | --- | --- |
| Licensing | Open source | Source-available (Sustainable Use License, fair-code) |
| The unit of work | An open-ended job an agent finishes | A fixed flowchart of nodes |
| Where a job runs | One isolated cloud computer per session, on its own branch | Your server or n8n Cloud |
| Configuration | Files in a git repo you own | Workflows in a database |
| Steps | Decided while the work runs | Drawn in advance on a canvas |
| Governance | Per-resource permissions for people and agents; approval gates; an audit trail | Role-based access, audit trails and human approvals |
| Models | Any provider with your own keys, or the ChatGPT plan you already pay for | OpenAI, Anthropic, Google or open-source models |
| Finished work | Opens a change request; merge is default-deny for agents | Runs the diagram |

The n8n rows come from n8n's own repository and documentation, [github.com/n8n-io/n8n](https://github.com/n8n-io/n8n), checked October 2026: it describes a fair-code platform under the Sustainable Use License, with model flexibility, human approvals and full observability. Kortix's rows come from the [Kortix docs](https://kortix.com/docs).

## When n8n is the right fit

Pick n8n when the job is a fixed flowchart: the same steps, in the same order, on every execution. A nightly sync, a form that becomes a ticket, or an invoice that files itself is exactly what a workflow engine is for.

## When Kortix is the right fit

Pick Kortix when the steps are decided while the work runs. Researching a market, reproducing an issue, or reconciling a month of records has no fixed path to draw in advance. Kortix hands that job to an agent that plans its own steps, calls your connectors as tools, and finishes by opening a change request. Session work reaches `main` through a change request, and merge is default-deny for agents.

## The short decision

A fixed flowchart with the same steps every time: n8n. Open-ended work that needs a plan of its own, on infrastructure you own: Kortix.
