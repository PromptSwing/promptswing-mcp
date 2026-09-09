# Importing a site from a repository

Already have the code somewhere? Connect the repository instead.

## 1 · Connect the repository

From the PromptSwing hosting dashboard. Every push to the selected branch is
released.

## 2 · What you get back

Each release writes a **GitHub Deployment** on the released commit — success or
failure, the address it is served at, and whether PromptSwing is hearing signals
from it. The repository is one-way no longer: the assistant that pushed the code
learns what happened without a PromptSwing login.

## 3 · Signals

**A page that was built elsewhere reports carts and orders only where it calls
the documented signal endpoints.** PromptSwing injects the library and the token
is real; whether your page calls it is your choice. `assess_site` — or the free
`POST /api/assess` — reports which calls are absent.

Contract: <https://api.promptswing.com/signals-spec.md>
