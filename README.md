# SDD Automation Status

External state repo for SDD loop engineering. Keeps automation JSON out of app repos so `ai-workflow` stays clean and multi-project state can share one repo.

## Layout

```
status/
  <ProjectName>/
    automation/
      state/
        active_work.json          # legacy summary
        active_spec_work.json     # spec lane
        active_feature_work.json  # feature lane
        active_idea_work.json     # idea lane
        blocked_work.json
```

## MMORPG_Web_App

Clone beside app repo (sibling `../status`):

```bash
git clone https://github.com/AIHeart-Professional/status.git ../status
```

Env (optional): `SDD_STATUS_REPO=../status` or absolute path.

State root: `{SDD_STATUS_REPO}/MMORPG_Web_App/automation/state/`

## Loop sync

After every lane state write in MMORPG_Web_App loops:

1. `cd` to status repo (`$SDD_STATUS_REPO` or `../status`)
2. `git add MMORPG_Web_App/automation/state/`
3. `git commit -m "chore(mmorpg): update <file> phase=<phase>"`
4. `git push`

Reports stay in app repo (`docs/automation/reports/`). Only state JSON lives here.

## Multi-project

Add `<OtherProject>/automation/state/` per app. Each JSON includes `"project": "<ProjectName>"`.
