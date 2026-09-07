# Synsema recipes

Programs that already work, ready to deploy on [synsema.com](https://synsema.com) in one click and then made your own. A recipe is a folder with a `syn.toml`; `catalog.toml` is the index synsema.com mirrors every hour.

## Recipes

| Recipe | What it is | Code |
|---|---|---|
| [lampson](lampson/) | The open-source coding agent, hosted: your own Lampson at a URL, with a workspace of its own. | [kitecosmic/lampson](https://github.com/kitecosmic/lampson) `v0.2.8` |

## How a recipe works

- `syn.toml` says what the code cannot say about itself: name, slug, version, kind (`web` or `worker`), the entry file, taglines, the secrets it needs (one line each, with what the value is for), optional `[env]` defaults and `[volumes]`.
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
