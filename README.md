# antifeed

A feed where **my own algorithm** — `algorithm/interests.md`, a markdown file — decides what I
see. A coding agent runs the sweep; the [social-wall](https://github.com/swapnilraj/social-wall)
engine does the deterministic parts. This repo holds only what is mine.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fswapnilraj%2Fantifeed&project-name=antifeed&repository-name=antifeed&env=WALL_USER,WALL_PASSWORD,WALL_COOKIE_SECRET,WALL_SYNC_TOKEN&envDescription=Basic-auth%20user%2Fpassword%20for%20your%20private%20wall%2C%20a%20random%20cookie%20secret%2C%20and%20a%20random%20machine%20token%20the%20sweep%20uses%20to%20sync%20(put%20the%20same%20token%20in%20your%20local%20.env)&envLink=https%3A%2F%2Fgithub.com%2Fswapnilraj%2Fantifeed%23hosted-wall&stores=%5B%7B%22type%22%3A%22blob%22%7D%5D)

**Easiest:** open this directory in `claude` or `codex` and say **"set this up"** — the agent follows
the engine's setup playbook (Vercel, browser, toolchain, R2, scheduling), asking you only for logins
and secrets. By hand:

**Easiest:** open this directory in `claude` or `codex` and say **"set this up"** — the agent follows
the engine's setup playbook (Vercel, browser, toolchain, R2, scheduling), asking you only for logins
and secrets. By hand:

```bash
npm install                      # pulls the engine
$EDITOR algorithm/interests.md   # your algorithm (required — the sweep refuses an empty profile)
cp .env.example .env             # hosted? WALL_URL + the WALL_SYNC_TOKEN you gave Vercel
npx antifeed doctor              # what works, what's optional
claude                           # or: codex — then say: run a sweep
npx antifeed build && open public/index.html
```

`npx antifeed prompt` prints a kickoff prompt if you'd rather script it: `claude -p "$(npx antifeed prompt)"` /
`codex exec "$(npx antifeed prompt)"`. Put that on a cron for a recurring sweep.

Optional layers, each a line or two in `.env` (see `.env.example`): a private hosted wall on
Vercel (`WALL_URL` + `WALL_SYNC_TOKEN`, read-state sync across devices), an Obsidian knowledge
base (`WALL_OBSIDIAN_VAULT`), self-hosted reel video (R2), and X / Instagram collection through `npx antifeed browser`
(a dedicated logged-in Brave/Chrome profile on the CDP port). The engine README covers each.

## Hosted wall

The Deploy button creates the Vercel project with `WALL_USER` / `WALL_PASSWORD` (your login),
`WALL_COOKIE_SECRET` (any long random string) and `WALL_SYNC_TOKEN` (another — the sweep's machine
token), and attaches a Blob store. Copy the deployment URL into `.env` as `WALL_URL` and the same
`WALL_SYNC_TOKEN` next to it; `npx antifeed doctor` confirms the two sides agree. Each sweep ends
with a push to `main`, which redeploys.

Updating the engine: `npm update antifeed` (or pin a tag in `package.json`).
