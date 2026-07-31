# Abel Benedict GitHub Profile — Setup Guide

## 1. Repository

Create/open the public GitHub repository:

`2171001`

This repository should be the profile repository for the GitHub account `2171001`.

## 2. Upload the project

Upload the complete folder structure exactly as provided:

```text
2171001/
├── .github/
│   └── workflows/
│       └── update-stats.yml
├── assets/
│   ├── activity.svg
│   ├── banner.svg
│   ├── github-stats.svg
│   └── top-languages.svg
├── scripts/
│   └── generate_stats.py
├── .gitignore
├── LICENSE
├── README.md
├── requirements.txt
└── SETUP.md
```

The three analytics SVGs are placeholders in the package. GitHub Actions will replace them with current values.

## 3. Commit

Commit the files to the default branch of the profile repository.

## 4. Enable workflow write permission

Open:

Repository → Settings → Actions → General

Under **Workflow permissions**, select:

**Read and write permissions**

Save the setting.

The workflow itself also declares:

```yaml
permissions:
  contents: write
```

The workflow uses GitHub's automatically provided `GITHUB_TOKEN`; no personal access token is required for this setup.

## 5. Run the workflow

Open:

Repository → Actions → Update GitHub Analytics

Select:

**Run workflow**

Wait for the job to finish successfully.

A successful run creates/updates:

```text
assets/github-stats.svg
assets/top-languages.svg
assets/activity.svg
```

The workflow then commits those generated files automatically.

## 6. Check the profile

Open:

`https://github.com/2171001`

The README should now display:

- the custom banner
- GitHub statistics
- top languages
- repository activity
- the cybersecurity profile content

## 7. Automatic updates

The workflow runs once per day at:

`00:17 UTC`

It can also be started manually at any time through:

Repository → Actions → Update GitHub Analytics → Run workflow

## 8. Why this setup works without github-readme-stats

The README does NOT request images from:

`github-readme-stats.vercel.app`

Instead it loads local files:

```markdown
./assets/github-stats.svg
./assets/top-languages.svg
./assets/activity.svg
```

GitHub Actions generates those files using the GitHub API and commits the results into the repository.

Therefore the profile does not depend on the paused Vercel deployment.

## 9. Local testing (optional)

From the repository root:

```bash
python -m venv .venv
```

Windows:

```powershell
.venv\Scripts\activate
```

Linux/macOS/WSL:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Set a GitHub token in your shell if you want to test locally.

PowerShell:

```powershell
$env:GITHUB_TOKEN="YOUR_TOKEN"
```

Bash:

```bash
export GITHUB_TOKEN="YOUR_TOKEN"
```

Then:

```bash
python scripts/generate_stats.py
```

The generated SVG files will appear under `assets/`.

## 10. Important operational note

The profile analytics are intentionally conservative. They show repository-level information that can be collected reliably through GitHub's REST API.

The activity card is a **repository activity card**, not a replacement for GitHub's native contribution heatmap.

The native contribution graph remains available on the GitHub profile itself.
