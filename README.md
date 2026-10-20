# Cursor Unofficial Android — Agent Rules

A small, **public, read-only** repository that holds the default "agent rule" used by the
[Cursor Unofficial Android](https://github.com/Foreverlegion/Cursor-Unofficial-Android) app.

**Heads up:** without a rule (either this default or your own file), you may lose some
functionality — the agent won't automatically know how to do certain things this app expects. If
you opt out, add your own rule file that explains how to do those things, or expect to spell them
out yourself each time.

This is nothing more than a "this is how you work with this app" note handed to Cursor. Nothing
here is secret, nothing here runs on your device. Feel free to fork it on your own GitHub and edit
to your heart's content.

## Why this exists

Cursor's account-level **User Rules** (Settings → Customize → Rules in the desktop app) are not
writable through the public Cursor API. The Android app only holds a Cloud Agents API key, and
that API has no endpoint to read or write your account User Rules. So the app can't set that rule
for you.

Instead, the app includes a rule as context in the **first message of each agent you start** —
it is *not* sent all the time, and it is not sent from the app's startup. It rides along only when
you kick off a new agent. This repo is the default source of that rule: a plain Markdown file
anyone can inspect.

## What's in here

- **`RULE.md`** — the actual rule text sent to the agent. This is the whole payload. Read it
  top to bottom; there's nothing hidden.
- **`README.md`** — this file.

That's it. No code, no scripts, no build steps, nothing that executes.

## How the app uses it

Three settings under **Settings → Chats & threads → Agent rule**:

1. **Use the default rule (this repo)** — the default. When you start an agent, the app includes
   the contents of `RULE.md` at the start of that agent's first message, so the agent reads it as
   standing context for that run.
2. **Use my own rule** — paste a URL to your own raw Markdown file (your own repo, a Gist, a raw
   file link). The app sends that file's contents instead. This is how you keep full functionality
   on your own terms.
3. **Don't use a rule** — the app sends no rule at all. Agents start with only your task prompt.
   Note: you may lose some functionality unless your prompts explain how to do those things.

You can switch between these at any time. The choice is stored on your device.

## Opting out

Pick **Don't use a rule** and the app stops attaching any rule to new agents. Existing agents are
unaffected. Be aware you may lose some functionality unless you add your own rule file (option 2)
that explains how to do the things the default rule covers.

## The cost

When a rule is enabled, its text is prepended to the first message of each new agent. A short rule
is a few hundred tokens and is negligible next to your actual task and the code the agent reads.
It's included once per agent launch and counts toward that agent's usage. To keep usage minimal,
opt out or keep your rule file short.

The rule is **context**, not an enforced account setting. A cloud agent reads it and generally
follows it, the same as any instruction you type.

## Privacy

- This repo contains no personal data and no secrets.
- The app reads `RULE.md` (or your own URL) and includes it in the agent prompt. It does not send
  your data to this repo, and this repo cannot receive anything from you.
- Nothing in this repo executes on your phone or anywhere else.

## Best option: paste it into a Cursor User Rule (zero tokens)

If you want this behavior **and** zero extra tokens on every agent spinup, do this once:
copy the text from `RULE.md`, paste it into a Cursor account **User Rule** on the desktop app,
then set the app to **Don't use a rule**. The agent gets the rule from your account, and the app
sends nothing extra. See `WALKTHROUGH.md` for a start-to-finish guide.

## Fork it

Feel free to fork this on your own GitHub and edit to your heart's content, then point the app at
your copy (option 2 above). You can view, clone, fork, and copy all of it freely.

## License

The rule text is free to copy and adapt. See `LICENSE` if present; otherwise treat the contents as
freely reusable with no warranty.
