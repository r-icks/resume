# LaTeX Resume Automation

This repository contains a LaTeX project for generating a resume, along with a GitHub Actions workflow that automatically compiles the PDF and uploads it to Dropbox. The workflow distinguishes between the `master` branch and `feature/*` branches to maintain separate PDFs.

---

## Features

- Compile LaTeX documents automatically on push.
- Upload resulting PDF to Dropbox.
- Automatically overwrite existing PDFs to keep links consistent.
- Masked access tokens for secure API usage.
- Branch-based PDF separation (`master.pdf` and `feature.pdf`).

---

## Workflow

The GitHub Actions workflow is triggered on:

- `push` to `master` → updates `/master.pdf` on Dropbox.
- `push` to any branch matching `feature/*` → updates `/feature.pdf` on Dropbox.

Steps include:

1. Checkout the repository.
2. Compile the LaTeX document using `xu-cheng/latex-action`.
3. Generate a Dropbox access token from the stored refresh token.
4. Upload the PDF to Dropbox using `curl`:
   - Overwrites the existing file.
   - Fails the workflow if the upload fails.
   - Access tokens are never printed in logs.

---

## Setup

### Dropbox App

1. Create a Dropbox App in [Dropbox App Console](https://www.dropbox.com/developers/apps).
2. Enable `files.content.write` scope.
3. Generate a **refresh token** for your app.

### GitHub Secrets

Store the following secrets in your repository:

- `DROPBOX_APP_KEY` → your Dropbox App Key
- `DROPBOX_APP_SECRET` → your Dropbox App Secret
- `DROPBOX_REFRESH_TOKEN` → refresh token generated in Dropbox

> **Note:** These secrets are used in the workflow and are masked in logs for security.

---

## Usage

1. Create or update your LaTeX file (`resume.tex`).
2. Push changes to either `master` or a `feature/*` branch.
3. GitHub Actions will automatically compile the PDF and upload it to Dropbox.
4. Use the shared Dropbox links to access the latest PDFs.

---

## Security Notes

- The workflow **never logs access tokens**.
- Only the repository workflow can use the secrets.
- Branch naming rules are enforced: only `master` and `feature/*` branches are allowed.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Contact

For questions or contributions, open an issue or submit a pull request.
