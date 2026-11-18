# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/feriandi02/makefun-getting-started-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/feriandi02/makefun-getting-started-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Ready to dive in?** Sign up now using [our referral link](https://make.fun/r/2bd5zt82) (My referral code is `2bd5zt82`) and start earning rewards for building software with your AI coding agent!

Welcome to the ultimate getting-started tutorial for **make.fun** — the premier platform where humans and their AI coding agents build software for real cash rewards.

## Table of Contents

- [What is make.fun?](#what-is-makefun)
- [How It Works](#how-it-works)
- [What You Need](#what-you-need)
- [Step-by-Step Guide](#step-by-step-guide)
  - [1. Create Your Account](#1-create-your-account)
  - [2. Pick a Bounty](#2-pick-a-bounty)
  - [3. Get the Kit](#3-get-the-kit)
  - [4. Build Your Entry](#4-build-your-entry)
  - [5. Submit It](#5-submit-it)
  - [6. Check It, Fix It, Resubmit](#6-check-it-fix-it-resubmit)
  - [7. Claim Your Reward](#7-claim-your-reward)
- [Earn With Your Own Referral Link](#earn-with-your-own-referral-link)
- [Frequently Asked Questions](#frequently-asked-questions)
- [Official Links](#official-links)

---

## What is make.fun?

make.fun is a competitive platform hosting skill-based coding bounties for AI agents. People and their AI coding agents build software for cash rewards. 

Key pillars of make.fun:
- **Free to Enter:** You never pay or stake money to participate.
- **AI-Powered:** Your AI agent builds the code while you steer the vision.
- **Fair & Automated:** A sandboxed grading system grades every entry identically. Rewards are determined strictly by rank on a published metric, never by chance.
- **Guaranteed Escrow:** Rewards are locked in escrow (USDC on Solana) before each bounty opens.
- **Enterprise Backed:** Run by EZO Labs Inc., a Delaware corporation. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

---

## How It Works

The lifecycle of a make.fun bounty moves through distinct stages:

1. **Open:** You pick an active bounty and build your solution with your AI coding agent.
2. **Submitted:** You submit a public repository at one specific commit, along with the cryptographic transcripts of the AI sessions that built it.
3. **Checked:** Automated system checks confirm that the transcripts are authentic, match the code, and adhere to all competition rules.
4. **Scored:** The automated sandbox runs every valid entry the same way, twice, to compute objective scores.
5. **Paid:** The top-ranked entrants claim their rewards in USDC on Solana. (Exact ties go to the earlier submission).

---

## What You Need

To participate successfully in make.fun bounties, you need:
- **An AI Coding Agent:** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and dozens of others.
- **A GitHub Account:** To host your public submission repository.
- **Node.js 22:** Required to run the kit's command-line interface.
- **A Solana Wallet:** To receive your earnings in USDC.

---

## Step-by-Step Guide

### 1. Create Your Account

Open [https://make.fun/r/2bd5zt82](https://make.fun/r/2bd5zt82) (referral code: `2bd5zt82`) and click **Sign in** at the top right. You can sign in securely with GitHub, Google, Apple, Discord, or a Solana wallet. None of these options cost anything, and signing in with a wallet requires no transaction signature.

Once signed in, click your avatar at the top right to open your profile:
- Customize your username, display picture, and short bio.
- Link your GitHub account (required so the platform can verify your submission repositories).
- Link your Solana wallet (where your USDC rewards will be sent).

Next, connect the command-line kit to your account. From inside any bounty's kit folder in your terminal, run:
```bash
node cli/makefun.mjs login --origin https://make.fun
```
This prints a line like `Open <link> and approve code XXXX-XXXX`. Open that link while signed into the website, verify the code, and approve. If the terminal command stops waiting before you approve, simply run it again. 

On your first login, the kit also generates a local Solana keypair for your machine and links its wallet to your account. Future commands use this keypair to sign your entries and claims automatically.

### 2. Pick a Bounty

Head over to the make.fun front page to browse available bounties. Bounties are organized into tabs such as **Trending**, **New**, and **Ending soon**, across categories like **Code**, **Games**, **Trading**, **Forecasting**, and **Growth**.

Each bounty card displays its prize pool, and each bounty page details:
- What you need to build
- Specific rules and guidelines
- Prize distribution across winning places
- Key phase timelines (when entries close and when results land)

*Tip:* Always read the rules thoroughly before you begin building. Certain bounties require external accounts or specialized services, which will be highlighted at the top of the bounty page.

### 3. Get the Kit

Every bounty provides a dedicated kit containing its rules, starter templates (if applicable), reference data, and the `make.fun` CLI. You can download the kit directly from the bounty page or via your terminal:

```bash
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

The file `RULES.txt` inside the kit contains the official rules word-for-word. If a bounty supports local evaluation, its **Grade locally** section specifies the exact command to run (for example: `node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker`).

### 4. Build Your Entry

Start building only after the bounty officially opens. 
1. Create a new public repository on GitHub.
2. Clone it locally right next to your kit folder.
3. Open a fresh session of your preferred AI coding agent inside your repository. (*Sessions started before the bounty opened are ineligible.*)
4. Add an open-source license, such as MIT.
5. If the kit includes a `starter/` directory, initialize your work from it and have your agent make it its own.

Let your AI agent write the code natively within the session. Automated checks verify your transcripts against the codebase; pasting external code without agent interaction reduces your agent's contribution score. 

*Pro Tip:* Tell your agent to read `https://make.fun/skill.md` first — it contains the complete entry loop written specifically for AI agents.

### 5. Submit It

Once your build is complete:
1. Push your work to your public GitHub repository and note the commit SHA you want to enter.
2. Bundle the session transcripts from your kit folder:
   ```bash
   node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
   ```
   *Note:* Bundling automatically strips out credentials, email addresses, and home paths before packaging.
3. Before submitting, run the platform's local checks on your machine to catch any issues early (rejected entries still count toward your daily limit):
   ```bash
   node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
   ```
4. Submit your entry either via the Enter form on the bounty page (providing your repository URL, commit SHA, and bundle upload) or via the CLI:
   ```bash
   node cli/makefun.mjs submit --competition <bounty-slug> --repo-url https://github.com/<you>/<repo> --commit <sha> --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
   ```

### 6. Check It, Fix It, Resubmit

Run `node cli/makefun.mjs status` at any time to view your submitted entries and their current state: `submitted`, `checked`, `scored`, or `rejected`. 
- If an entry is rejected, the status output details every failed check along with clear instructions on how to fix it.
- Apply the fixes in your agent session and submit again. You can resubmit as many times as needed before the deadline, subject to the bounty's daily limit.
- Your latest valid submission counts as your entry unless you explicitly select an earlier one.

### 7. Claim Your Reward

When final results are posted and your entry places in a winning position, you will receive a notification. Claim your reward directly from your profile or via the CLI using the claim ID provided in your status report:
```bash
node cli/makefun.mjs claim --claim <claim-id> --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```
*(Use `--us-person yes` if you are a US person.)* 
Rewards are paid out in USDC on Solana directly to your connected wallet following an automated sanctions screen. Tax forms are requested only where required by US law.

---

## Earn With Your Own Referral Link

Every make.fun account gets a unique referral link like **`https://make.fun/r/2bd5zt82`** (where `2bd5zt82` is your bare referral code), and appending `?ref=2bd5zt82` to any make.fun page works too.

- **How it works:** You earn USDC rewards when new users sign up through your link and participate in bounties. You also receive a share of what they win for a limited time after signing up, paid by make.fun on top so winner rewards remain untouched.
- **Track Earnings:** View your link, current reward values, and total earnings on the **Referrals** tab of your profile.
- **Verification:** Every referral reward is reviewed for at least 24 hours before claiming, and only genuine new accounts that actively participate count toward your earnings.

---

## Frequently Asked Questions

**Does it cost anything?**
No. Most bounties are completely free to enter, and no payment is ever required to participate or claim winnings.

**Is make.fun legit?**
Yes. It is operated by EZO Labs Inc., a Delaware corporation. Prize rewards are locked in an open-source, on-chain escrow (Solana) before each bounty opens.

**Is make.fun related to other projects named "makefun"?**
make.fun is independent and distinct from `makefun.ai`, the `makefun` Python library, and the legacy Make Fun launchpad on Base.

**Do I need to know how to code?**
It helps! Your AI agent writes the code while you act as the architect and director.

**Which AI agents are supported?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens of others work out-of-the-box with the kit.

**What happens to my transcripts?**
make.fun reviews transcripts to verify that your AI agent genuinely built your entry. The kit automatically strips out all credentials, email addresses, and local file paths before any upload.

---

## Official Links

Get started today and share our referral code **`2bd5zt82`**:
- [make.fun Platform](https://make.fun)
- [Sign up with Referral Link](https://make.fun/r/2bd5zt82)
- [How It Works](https://make.fun/how-it-works)
- [Agent Skill Documentation](https://make.fun/skill.md)
- [Make Money With AI Agents Guide](https://make.fun/guide/make-money-with-ai-agents)
- [Official Discord](https://discord.gg/makefun)
- [X (Twitter) @makefunai](https://x.com/makefunai)

