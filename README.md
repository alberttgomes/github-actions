# GitHub Actions for liferay-upgrades

Automated workflows for the `liferay-upgrades` organization.

Copied and adapted from: https://github.com/liferay-page-management/github-actions

## Sync liferay-portal Fork

`.github/workflows/sync-liferay-portal.yml` is a cron job that runs hourly to sync
`liferay-upgrades/liferay-portal` (`master`) from the upstream `liferay/liferay-portal`.

### Setup

The sync step calls `gh repo sync` against a repository other than the one hosting the
workflow, so the default `GITHUB_TOKEN` is not sufficient. Create a Personal Access Token
and expose it as a repository secret named `SYNC`:

1. Generate a token with the `repo` scope (classic) or read/write **Contents** on
   `liferay-upgrades/liferay-portal` (fine-grained).
1. In this repository, add it under **Settings > Secrets and variables > Actions** as
   `SYNC`.

### Schedule

The workflow runs at the top of every hour (UTC) and can also be triggered manually from
the **Actions** tab (`workflow_dispatch`). The `workflow-keepalive` job keeps the scheduled
trigger from being disabled after 60 days of repository inactivity.
