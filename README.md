# eval-collab-etienne

Training repository for collaborative GitHub workflows. Covers issue management, pull request reviews, Conventional Commits, and architectural decision records.

## Prerequisites

- Git
- A GitHub account with write access to this repository

## Installation

```bash
git clone https://github.com/MrVohi/eval-collab-etienne.git
cd eval-collab-etienne
```

## Usage

Follow the exercise steps provided by your instructor. Each step targets a specific GitHub workflow:

1. Repository setup (branch protection, CODEOWNERS, issue templates)
2. Bug / incident issue
3. Pull request review with Conventional Comments
4. Documentation (README, ADR, AGENTS.md)

## Stack

- Docker — services run as containers
- WireGuard — VPN on `vpn-01`, UDP port 51820
- Reverse proxy — see [ADR-0001](docs/adr/0001-reverse-proxy.md) for the Nginx vs Traefik decision

## Contributing

See [AGENTS.md](AGENTS.md) for contribution guidelines, conventions, and forbidden actions.

## License

MIT — assumed, to be confirmed with the repository owner.
