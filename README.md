# Clinic Express Booking & Check-In Hub

A lightweight, mobile-first sales prototype for Varangian Digital. It is a static site: there is no build step, backend, package install, or third-party runtime dependency. The interactive booking, WhatsApp confirmation, and receptionist webhook are demo simulations; the form does not transmit or store patient details.

## Customize a prospect link

Set query parameters on the hosted `index.html` URL:

| Parameter | Values | Default |
| --- | --- | --- |
| `clinic` | URL-encoded practice name | `Your Practice Express Hub` |
| `type` | `dental`, `optom`, or `aesthetic` | `dental` |
| `phone` | Practice WhatsApp number, international digits (no `+`) | WhatsApp opens without a preset recipient |

Example links (replace the domain with your deployed URL):

```text
https://your-domain.example/?type=dental&clinic=Harbour%20Dental
https://your-domain.example/?type=optom&clinic=City%20Optical
https://your-domain.example/?type=aesthetic&clinic=Willow%20Skin%20Studio
https://your-domain.example/?type=dental&clinic=Harbour%20Dental&phone=27820000000
```

`URLSearchParams` handles spaces encoded as `+` as well as `%20`. The WhatsApp action opens a chat with a pre-filled message; it does not send anything until the visitor chooses to send it in WhatsApp.

## Run locally

Open `index.html` directly in a browser, or serve this directory with any static file server. No build is required.

## Deploy

For GitHub Pages, authenticate with `gh auth login`, then run this from `clinic-demo-hub/`. It creates a public repository, pushes the site, and enables Pages from the `main` branch:

```sh
git add index.html README.md && git commit -m "Add Clinic Express Booking Hub demo" && git branch -M main && gh repo create clinic-demo-hub --public --source=. --remote=origin --push && gh api "repos/$(gh api user --jq .login)/clinic-demo-hub/pages" --method POST -F build_type=legacy -F "source[branch]=main" -F "source[path]=/"
```

GitHub Pages publishes at `https://YOUR-USER.github.io/clinic-demo-hub/` after its first deployment completes. Replace `YOUR-USER` with your GitHub username when building prospect links.

For Vercel CLI, authenticate first if needed, then run from this directory:

```sh
vercel --yes --prod
```

For Netlify CLI, authenticate and link/create a site once with `netlify init`, then deploy from this directory:

```sh
netlify deploy --prod --dir=.
```

Use the HTTPS URL returned by your provider and append the desired query parameters to create a prospect-specific link.
