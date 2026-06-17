# accountability

A tiny vape accountability tracker for Brian, Karla, and Graeme.

Open the app, pick your name, answer "did you vape yesterday" yes/no. The dashboard shows a 30-day grid for all three of us plus our collective streak (consecutive days where everyone logged "no").

## How sync works

State lives in a **secret GitHub Gist** on `graeme120`. The app reads and writes the gist via the GitHub API using a Personal Access Token (PAT) that each person stores in their browser's `localStorage` (never in source code).

## Setup (one time, Graeme only)

1. Generate a fine-grained PAT at https://github.com/settings/tokens?type=beta
   - **Repository access:** none needed
   - **Account permissions → Gists:** Read and write
   - **Expiration:** 90 days (or longer if you trust the share channel)
2. Share that token with Brian and Karla via Signal/iMessage (not Slack/email)

## Setup (one time, each person)

1. Open the deployed URL
2. Paste the token Graeme sent you
3. Tap "connect"

That's it. The token stays in your device's `localStorage`. You can clear it any time from the settings gear.

## Daily use

1. Open the URL
2. Tap your name
3. Tap yes or no
4. See the dashboard

The dashboard auto-syncs on open. Hit "refresh" to pull in the others' latest logs.

## Local development

It's a single static HTML file. Just open `index.html` in a browser. Skip the token entry and click "just view (offline)" to use localStorage-only mode.

## Resetting

- **Local only:** settings gear → "reset everything" wipes your device's cache + token
- **Everyone's data:** edit the gist at https://gist.github.com/graeme120/387432bdc79a415f7ec301a58aa5e7ec directly, replace contents with `{"days": {}}`

## Conflict handling

When you log an entry, the app fetches the latest remote state, applies your change, and pushes the merged result. Three people logging within the same few hundred ms could in theory clobber each other — for a once-a-day app among 3 people, this isn't worth solving properly.
