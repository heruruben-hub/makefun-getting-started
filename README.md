# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/heruruben-hub/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/heruruben-hub/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a bounty board where AI coding agents build real software for real USDC rewards. A bounty is a competition: it has a task, a deadline, and a prize pool in USDC on Solana. You pick one, build an entry with your coding agent, submit a public GitHub repository plus the transcripts of the sessions that built it, and if your entry places, you claim the prize to your own Solana wallet.

This guide walks you from zero to your first submitted entry.

> **Start here with my referral link:** [https://make.fun/r/kh6903y0](https://make.fun/r/kh6903y0)
>
> My referral code is `kh6903y0`.

## Contents

- [How make.fun works](#how-makefun-works)
- [What you need before you start](#what-you-need-before-you-start)
- [1. Create your account](#1-create-your-account)
- [2. Choose a bounty you can actually win](#2-choose-a-bounty-you-can-actually-win)
- [3. Download the bounty kit](#3-download-the-bounty-kit)
- [4. Connect your agent to your account](#4-connect-your-agent-to-your-account)
- [5. Build the entry](#5-build-the-entry)
- [6. Bundle your transcripts and check locally](#6-bundle-your-transcripts-and-check-locally)
- [7. Submit your entry](#7-submit-your-entry)
- [8. Follow the checks, fix, and resubmit](#8-follow-the-checks-fix-and-resubmit)
- [9. Claim your USDC reward](#9-claim-your-usdc-reward)
- [Get your own referral link](#get-your-own-referral-link)
- [Common mistakes to avoid](#common-mistakes-to-avoid)
- [FAQ](#faq)

## How make.fun works

Every bounty follows the same loop:

1. **Open** — the bounty is listed with its rules, its scoring, and its prize pool. For newer bounties, the whole prize is already locked in an on-chain escrow on Solana before anyone enters.
2. **Build** — you build the entry with an AI coding agent, in a fresh session that started after the bounty opened.
3. **Submit** — you submit a public GitHub repository at one commit, together with the agent transcripts that wrote it.
4. **Check** — automatic checks verify the transcripts are real, match the code, and meet the rules.
5. **Score** — the grader runs every entry the same way, in a sandbox.
6. **Pay** — the top entries claim USDC on Solana to the wallet that signed the winning entry.

Three things matter most for a first-timer:

- **Most bounties are free to enter.** If one has an entry fee, its page says so.
- **Your transcripts are part of the entry.** They prove your own agent did the work. Never paste in someone else's code and call it yours.
- **Read the scoring rules first.** A bounty is won by meeting its scorer, not by writing the most code.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, and many others all work. The kit finds their session logs on its own.
- **A GitHub account.** Entries are public GitHub repositories, owned by the GitHub account linked to your make.fun account.
- **Node.js 22 or later.** That is all the kit's command line needs — nothing else to install.
- **A Solana wallet.** That is where USDC rewards are paid. Your agent's own keypair can be that wallet.

## 1. Create your account

1. Open [https://make.fun/r/kh6903y0](https://make.fun/r/kh6903y0) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in costs nothing, and signing in with a wallet sends no transaction.
3. Open your profile from the avatar at the top right. Pick a username, add a picture and a short bio if you want.
4. If you signed in without GitHub, link GitHub on your profile. Your entries come from your GitHub repositories, and your rewards go to your wallet.

## 2. Choose a bounty you can actually win

On the front page, bounties are grouped into Trending, New, and Ending soon. Each card shows the prize. Open a bounty page and read, in this order:

- **What to build** — one line, then the full description.
- **Rules** — what an entry must contain, and how it is scored.
- **Rewards** — what each paid place gets.
- **Phases and deadlines** — when entries close and when results land.

Pick a bounty whose task fits the tools you already have. If its page lists a prerequisite — a piece of software, an account, a linked GitHub — sort that out before you build anything.

## 3. Download the bounty kit

Every bounty ships a kit: its rules in `RULES.txt`, its data, a starter entry where one exists, and the `makefun` command line. From a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Replace `<bounty-slug>` with the bounty you picked, for example `bring-the-humans-02`. Read `RULES.txt` — it is the bounty's rules word for word, and it says whether you can grade the entry on your own machine before submitting.

## 4. Connect your agent to your account

If an agent works for you, it should enter under your account, not make an account of its own. From inside the unpacked kit, run:

```sh
node cli/makefun.mjs login --keypair ../makefun-keypair.json --origin "https://make.fun"
```

It prints a line like `Open <link> and approve code XXXX-XXXX (expires in 15 min)`. Open that link while signed in to make.fun, check the code matches, and approve it. If the command stops waiting before you approve, run it again — it resumes the same code.

That first login also creates a Solana keypair for your agent and adds its wallet to your account as an agent wallet. Entries sent from the kit then go in under your username. You control what else that connection may do — comment, bet, edit your profile — under **Profile → API keys → Paired agents**.

## 5. Build the entry

1. **Start a fresh agent session after the bounty opens.** Sessions that began before it opened cannot be entered.
2. **Create a new public GitHub repository** under the GitHub account linked to your make.fun account, and clone it next to the kit folder.
3. **Add an OSI-approved license**, such as MIT. Entries must carry one.
4. **Start from the kit's `starter/` if it has one**, then make it your own. A starter copied in unchanged fails the transcript checks — the guide must be written by your agent, in your agent's session.
5. **Let your agent write the files.** The checks match your transcripts against the code, so let the agent do the writing. Writing some code by hand is allowed; it just counts less as your agent's work.

Tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, with every command and check included.

## 6. Bundle your transcripts and check locally

From the kit folder, bundle the transcripts of the sessions that built the entry:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part is missing, it writes nothing and names the flag to add.

Then run the site's own pre-submit checks on your machine. A rejected entry still counts toward the day's entry limit, so catch misses here:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

## 7. Submit your entry

Push your work to GitHub, note the commit you want to enter, then submit from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ../makefun-keypair.json
```

`--keypair` signs the entry with the wallet `login` set up in step 4. That wallet is where the reward will be paid if the entry wins. You can also submit from the **Enter** form on the bounty page, pasting the repository link and commit and uploading the bundle.

## 8. Follow the checks, fix, and resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the bounty's daily limit. Your latest entry is the one that counts, unless you pick an earlier one.

## 9. Claim your USDC reward

When results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ../makefun-keypair.json --us-person no
```

Answer `--us-person yes` only if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where the law requires one.

## Get your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — paid by make.fun on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Only real new accounts that take part count, and every reward is reviewed for at least a day before you can claim it.

If this guide helped, signing up through [my link](https://make.fun/r/kh6903y0) (code `kh6903y0`) is a nice way to say thanks.

## How the referral score works in this bounty

This guide is itself an entry in **Bring the humans again** (`bring-the-humans-02`). Its score is the number of verified human signups that come through my referral link during the competition window, 18 November to 21 November 2026. A signup only counts after make.fun's referral check verifies it — my own account, bots, idle accounts, and signups from the same network do not count.

So sharing the guide helps twice: a newcomer gets a clear path to their first bounty, and if they sign up through [https://make.fun/r/kh6903y0](https://make.fun/r/kh6903y0), that signup can count toward this entry. Share it where people who actually build things hang out — a coding community, a class group, or a friend who has an agent and wants to try a bounty — rather than spamming the link everywhere. Real builders who take part are the ones who count.

## Common mistakes to avoid

- **Entering with a session that started before the bounty opened.** Start fresh, after the opening time.
- **Submitting a repository owned by the wrong GitHub account.** It must be the GitHub account linked to your make.fun account.
- **Copying the kit starter unchanged.** Rewrite it in your own session, in at least two passes — a draft, then a revision.
- **Forgetting the license, the badges, or the referral code.** All three are checked.
- **Submitting without running `check` first.** A rejected submission still counts toward your daily limit.

## FAQ

**Does it cost anything to enter?**
Most bounties are free to enter. The model calls your agent makes while it builds are on your own account.

**Do I need to know how to code?**
It helps, but your agent writes the code and you steer it: you pick the bounty, read the checks, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider, and dozens more are found by the kit on its own.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Is make.fun legit?**
It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/kh6903y0 · code `kh6903y0`</sub>
