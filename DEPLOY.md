# Deploying this site to Netlify

This repository is a simple static site (single `index.html`). Below are a few options to deploy or update the site on Netlify.

1. Quick: Drag-and-drop

- Open https://app.netlify.com/drop
- Drag the repository folder (or the built site folder) into the browser area. Netlify will upload and publish it immediately.

2. Netlify CLI (manual deploy)

- Install Netlify CLI locally:

```powershell
npm install -g netlify-cli
# or use npx for a one-off:
npx netlify-cli deploy --dir=. --prod
```

To do a production deploy (recommended with auth):

```powershell
# login once interactively
npx netlify-cli login

# then deploy from repo root
npx netlify-cli deploy --dir=. --prod --site <SITE_ID>
```

3. Automatic deploy from GitHub (CI)

- This repo includes a GitHub Actions workflow at `.github/workflows/deploy-netlify.yml` which runs on `push` to `main`.
- To make it work, add two repository secrets in GitHub:
  - `NETLIFY_AUTH_TOKEN` — a personal access token from Netlify (create it in your Netlify user settings > Applications > Personal access tokens).
  - `NETLIFY_SITE_ID` — the Site ID from your Netlify site (Site settings > Site information).

Once those secrets are configured, pushing to `main` will trigger the workflow which runs `netlify deploy --dir=. --prod`.

Troubleshooting

- If the workflow fails, check the Actions tab in GitHub to see logs. Common issues are wrong secrets or missing site ID.
- You can also test the netlify-cli deploy locally to confirm credentials and site ID are correct before enabling CI.

If you want, I can:

- Add a simple badge to `index.html` or `README` showing the Netlify site URL once you have the site deployed.
- Remove the workflow if you prefer only manual deployments.
