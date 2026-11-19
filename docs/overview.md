# Overview

Source: this repo, `docs/overview.md`. The company library, when it mirrors product docs, should copy this file rather than rewrite it.

Invasion Of Zombies is a free, offline, chibi zombie crowd-runner for Android (`com.invasionofzombies.app`). This repository is the public website players and the Play listing land on. It explains the game and links to Google Play. It does not run the game, hold accounts, or take payment.

Who it is for: someone deciding whether to install the game, and Google Play's website and privacy-policy links.

## Repo roles

- **This repo** (`invasionofzombies-site`) is the site at invasionofzombies.com.
- **`invasionofzombies`** is the Capacitor Android package. Game files live in its `www/` directory. Its `CLAUDE.md` names this site as the sibling.
- **`invasionofzombies-dev`** is an empty repository. The usual Ubersoft layout puts source in `-dev`. That has not been done for this game. Do not document a source tree that is not there.

## Who edits what

Engineering changes the pages. DevOps reviews the publish path (Pages, domain, anything that would expose repo files). QA reviews the result. QA & Security owns a changelog if one is added; this repo does not have `changelog.md` or `changelog.txt`. The CEO merges after the clearance line in `ubersoft-company` `company/audit/cleared.md` and an explicit go. Nothing in this repo is a Punchi Park or Punchi Guide path.

The privacy policy is public legal copy. A change to its wording updates the effective date in `privacy.html`. Store-listing text and the game changelog live with the game and with QA, not in this site repo.
