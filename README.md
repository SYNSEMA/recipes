# Synsema recipes

Programs that already work, ready to deploy on [synsema.com](https://synsema.com) in one click and then made your own. A recipe is a folder with a `syn.toml`; `catalog.toml` is the index synsema.com mirrors every hour.

## Recipes

| Recipe | What it is | Code |
|---|---|---|
| [lampson](lampson/) | The open-source coding agent, hosted: your own Lampson at a URL, with a workspace of its own. | [kitecosmic/lampson](https://github.com/kitecosmic/lampson) `v0.2.8` |
| [vela-app](vela-app/) | A confidential app for Horizen's Vela: the guest with its tests, and a workbench that deploys it and drives it from the browser — register, deposit, encrypted payloads, events, reports. On the public devnet out of the box. | [SYNSEMA/vela-app](https://github.com/SYNSEMA/vela-app) `v0.2.0` |
| [vela-payroll](vela-payroll/) | Private payroll on Vela: a web console where an employer funds, onboards people and runs payroll in a stablecoin; each person's payslips and payouts are one page away. On the public devnet out of the box. | [SYNSEMA/vela-payroll](https://github.com/SYNSEMA/vela-payroll) `v0.2.2` |
| [vela-treasury](vela-treasury/) | An agent treasury on Vela: a web console where the owner sets the policy, an agent proposes payments, the enclave pays what fits through a trigger contract and holds the rest for the owner's approval. On the public devnet out of the box. | [SYNSEMA/vela-treasury](https://github.com/SYNSEMA/vela-treasury) `v0.2.1` |
| [vela-auction](vela-auction/) | A sealed-bid auction on Vela: a web console with the seller's desk and a desk per bidder; encrypted bids, matching inside the enclave, settlement from escrow; losing bids are never revealed. On the public devnet out of the box. | [SYNSEMA/vela-auction](https://github.com/SYNSEMA/vela-auction) `v0.2.1` |

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
