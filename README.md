# Synsema recipes

Programs that already work, ready to deploy on [synsema.com](https://synsema.com) in one click and then made your own. A recipe is a folder with a `syn.toml`; `catalog.toml` is the index synsema.com mirrors every hour.

## Recipes

| Recipe | What it is | Code |
|---|---|---|
| [lampson](lampson/) | The open-source coding agent, hosted: your own Lampson at a URL, with a workspace of its own. | [kitecosmic/lampson](https://github.com/kitecosmic/lampson) `v0.2.8` |
| [vela-policy-engine](vela-policy-engine/) | A payment policy engine on Horizen's Vela: a web console where the owner sets the spending policy, an AI agent reviews invoices and proposes payments, the enclave pays what fits through a trigger contract and holds the rest for the owner; the agent never holds a key. On the public devnet out of the box. | [SYNSEMA/vela-policy-engine](https://github.com/SYNSEMA/vela-policy-engine) `v0.3.0` |
| [vela-dark-pool](vela-dark-pool/) | A dark pool for block trades on Horizen's Vela: a web console with the seller's desk and a desk per buyer; orders go in encrypted, the enclave matches them, settlement from escrow; nobody sees the book, losing orders are never revealed. On the public devnet out of the box. | [SYNSEMA/vela-dark-pool](https://github.com/SYNSEMA/vela-dark-pool) `v0.3.0` |
| [vela-payroll](vela-payroll/) | Private payroll on Horizen's Vela: a web console where an employer funds, onboards people and runs payroll in a stablecoin; nobody outside sees who earns what, each person's payslips and payouts are one page away, an auditor gets the report. On the public devnet out of the box. | [SYNSEMA/vela-payroll](https://github.com/SYNSEMA/vela-payroll) `v0.2.6` |
| [vela-transfers](vela-transfers/) | Private transfers on Horizen's Vela: balances and transfers encrypted in the enclave, an invoice and a public receipt per transfer, the history for an allowed auditor; the starter kit for any Vela app, with a workbench that drives it from the browser. On the public devnet out of the box. | [SYNSEMA/vela-transfers](https://github.com/SYNSEMA/vela-transfers) `v0.4.0` |

## How a recipe works

- `syn.toml` says what the code cannot say about itself: name, slug, version, kind (`web` or `worker`), the entry file, taglines, the secrets it needs (one line each, with what the value is for), optional `[env]` defaults, `[volumes]`, `[provision]` (`env_url = "https://…"`: a URL the control asks when the project is created, whose `env` object seeds the environment — a devnet handing out a token; Environment has a button to ask it again), and `[hosts]` — the extra names a web service answers to (`api = "what it is for"` → `<project>-api.synsema.app`, handed to the program as `SYNSEMA_HOST_API` for a `host env(…)` block).
- The code lives in the folder itself or, with `[source]`, in another public repository at a tag. The `require` block of the entry file is the manifest of capabilities; it is never repeated here.
- Deploying a recipe copies its files into the user's account at the version listed. A recipe that changes later does not change projects already created; the dashboard offers the update.

## Add, edit, remove

- **Add:** a folder with `syn.toml` and a `[[recipe]]` entry in `catalog.toml`. Open a pull request.
- **Edit:** push to the folder, or move `[source] ref` to a new tag. Raise `version` when users should get the change.
- **Remove:** delete the entry from `catalog.toml`. The folder can stay; existing projects do not depend on it.

## Your repository as a recipe

Any public repository with a `syn.toml` at its root can carry the button. It enters this catalog when added to `catalog.toml`.

```markdown
[![Deploy on Synsema](https://synsema.com/assets/deploy-button.svg)](https://synsema.com/new?repo=https://github.com/you/your-agent)
```
