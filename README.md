# The Tablekeeper — public CI control repository

This repository contains **workflow configuration only**. The application source code, tests, migrations and build artifacts remain in the private repository `Sidious92/The-Tablekeeper`.

## How it works

The `tablegate-private-ci.yml` GitHub Actions workflow checks out a **specific 40-character commit SHA** from the private repository using the GitHub Actions secret `THE_TABLEKEEPER_TOKEN`. The checkout uses `persist-credentials: false`.

Its jobs validate build/TypeScript/Vitest, Atlas browser smoke, and isolated local Supabase SQL/RLS/Storage; the SQL job is restricted to a disposable local Docker database. No production environment, deployment credential or paid AI provider is supplied.

**Public logs must never print private build/test output, source excerpts, private environment files or uploaded screenshots/artifacts.** A failed job reports only the failing stage. To diagnose a failure, reproduce that pinned SHA in a trusted private environment.

## Running a check

Go to **Actions → TableGate pinned private CI → Run workflow**, and paste the exact commit SHA to test, or use the pinned default SHA in the workflow. The SHA is verified before the private checkout. A workflow push runs the currently pinned SHA when this workflow file changes.

Never put `THE_TABLEKEEPER_TOKEN` or its value in a tracked file. The secret must have only **read-only Contents** access to `Sidious92/The-Tablekeeper`, and should be revoked/rotated if it has wider scopes than required.

This public repository is **not** an application release, deployment source or public code mirror. GitHub Actions availability and usage rules remain subject to the account's plan and applicable terms.
