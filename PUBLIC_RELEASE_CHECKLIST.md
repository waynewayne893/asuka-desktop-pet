# Public Release Checklist / 公开发布前检查清单

> Current status: **PRIVATE ARCHIVE — NOT APPROVED FOR PUBLIC RELEASE.**
>
> This repository contains third-party fan-made character assets. The existing
> README and `ASSET_RIGHTS.md` prohibit public redistribution without permission.

A future public release must satisfy every item below. Do not change GitHub
visibility until all items are checked and the owner gives explicit approval.

## 1. Rights and licensing

- [ ] Written permission from the applicable character/franchise rights holders
      for every third-party character asset, or the assets are removed/replaced.
- [ ] Asset inventory completed (`ASSET_RIGHTS.md`).
- [ ] Asset-specific license/attribution added for all remaining assets.
- [ ] Repository-level `LICENSE` reviewed; it must not imply rights the owner
      does not have.
- [ ] Third-party fonts, sounds, models, icons, and reference images audited.

## 2. Content cleanup

- [ ] All private/local absolute paths replaced with placeholders.
- [ ] Usernames, local machine details, internal handoff logs and private
      operational notes reviewed/removed.
- [ ] Personal data and confidential project information removed.
- [ ] Unused `work/` process files remain excluded.
- [ ] Public-facing README explains what the project is and what it is not.

## 3. Security

- [ ] Full Git history scanned for credentials, tokens, private keys and secrets
      (not only the current tree).
- [ ] Any leaked credential rotated immediately; history cleaned if needed.
- [ ] Image metadata/EXIF reviewed for personal information.
- [ ] Dependency and build instructions reviewed; no private registry or token
      dependency.

## 4. History and visibility

- [ ] Third-party assets removed from **all commits** (history rewrite or clean
      repository), not only from the current HEAD.
- [ ] Force-push/rewrite plan reviewed and backed up.
- [ ] Forks/caches/indexing implications understood; public exposure cannot be
      perfectly recalled by switching back to Private.
- [ ] Explicit owner approval recorded before changing visibility.

## 5. Repository presentation

- [ ] Public README with scope, limitations, and installation/reproduction
      expectations.
- [ ] LICENSE, asset attribution, contribution/security guidance.
- [ ] Release/download method defined if users need a runnable artifact.
- [ ] No claim that this repo can rebuild the pet from a clean clone unless true.

## Decision

Until this checklist is complete:

```text
Visibility: Private
Public redistribution: Prohibited
Repository role: Private archive / rights-cleared material only
```
