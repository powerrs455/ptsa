# PTSA Tool & Machine Manager — GitHub source pack

## Included

- `index.html` — the original standalone frontend HTML that was available for packaging.
- `backend/index.ts` — the current AppDeploy shared-state API source, including the state keys for inventory, loans, machines, announcements, modules, enrollments and results.
- Vite, TypeScript, Tailwind and package configuration.
- This README with setup and deployment notes.

## Important source-parity note

This package was assembled from the locally available uploaded HTML plus the current backend source snapshot. The uploaded HTML is an earlier standalone frontend; it is **not byte-for-byte identical** to the latest deployed AppDeploy `index.html`. Therefore, do not treat this ZIP as a verified full export of every latest deployed UI feature. In particular, the latest app's modules/results and latest theme adjustments may not all be present in this older HTML file. The AppDeploy backend uses `@appdeploy/sdk`; it will not run unchanged on GitHub Pages or a generic Node host without adapting the API/database layer.

Live app: https://ptsa-tool-machine-manager-zmafh0.v2.appdeploy.ai/

## Run the standalone HTML locally

1. Extract the ZIP.
2. Open `index.html` in a modern browser.
3. This is useful for reviewing the standalone frontend, but local browser storage is not shared across different users or devices.

## Upload to GitHub

1. Create a repository on GitHub.
2. Extract this ZIP on your computer.
3. Upload the extracted files and folders to the repository root (so `index.html` is at the root), then commit.
4. If you only want a static preview, enable **Settings → Pages** and publish from the `main` branch and `/ (root)`.

## Backend and full multi-user deployment

GitHub Pages only serves static files; it does not execute the AppDeploy backend or provide the shared database. To retain cross-user tool/machine sign-out requests, storeman approvals, announcements and shared results, deploy the frontend and backend to a compatible application host and connect the API to an authenticated database. The current backend imports `@appdeploy/sdk` and relies on AppDeploy's `router`, `json`, `error`, and `db` services, so it must remain on AppDeploy or be ported to another backend/database stack.

## Security warning

Do not use the included shared-state API as the sole security boundary for official student results or sensitive records. The current shared-state design needs robust server-side authentication, role-based authorization, school-level scoping, validation and audit controls before production use.

## Basic checks

- Confirm `index.html` opens.
- Review browser console errors.
- Before using real school data, validate role permissions, data persistence, backup/restore, access controls and the full student/storeman/lecturer workflows in the deployed environment.
