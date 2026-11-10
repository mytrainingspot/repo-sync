# repo-sync

Keeps `master`, `staging` and tags identical between `mytrainingspot/my-training-spot` (where work happens) and `yoltlabs/my-training-spot` (where production builds from), in both directions, fast-forward only.

- Runs every 5 minutes, or from **Actions → Sync → Run workflow**.
- Never forces. If both repos changed the same branch, the run fails, nothing is pushed, and GitHub emails the failure.
- Nothing is added to either project repo.

## Setup

- Secret `ORG_SYNC_TOKEN`: classic token, scopes `repo` + `workflow`, from an account that can push to both repos.
- Variable `SYNC_DRY_RUN=true` makes every run a dry run. Delete it to go live.

## Locally

`./repo-sync --dry-run` uses your SSH access to both repos.

To resolve a divergence, in the project checkout:

```
git fetch yolt && git switch <branch> && git merge yolt/<branch> && git push origin <branch>
```

The next run syncs it.
