# Walkthrough: Make the app's rule a Cursor User Rule (zero extra tokens)

This is the recommended setup. You paste the rule into Cursor's account-level **User Rules** once,
then tell the app to stop sending its own rule. After that, every agent you start already has the
rule (because Cursor applies account User Rules to cloud agents), and the app adds **no extra
tokens** to your agent spinups.

You only need to do this once.

---

## Step 1 — Copy the rule text

1. Open [`RULE.md`](./RULE.md) in this repo.
2. Click the **Raw** button (top-right of the file view) to get the plain text.
3. Select all (`Ctrl`/`Cmd` + `A`) and copy (`Ctrl`/`Cmd` + `C`).

## Step 2 — Open Cursor's User Rules

On the **Cursor desktop app** (not the phone — the account User Rules editor lives here):

1. Open **Settings** (gear icon, or `Ctrl`/`Cmd` + `Shift` + `J`).
2. Go to **Rules** (under "Customize" / "Rules & Memories" depending on your version).
3. Find the **User Rules** section. This is the account-level rule that applies everywhere,
   including cloud agents.

## Step 3 — Paste it in

1. Click into the **User Rules** box.
2. Paste the text you copied (`Ctrl`/`Cmd` + `V`).
3. If you already have User Rules, add this below them (or merge as you like). Keep one copy —
   don't paste it twice.
4. Save / close settings. Cursor stores User Rules automatically.

## Step 4 — Turn off the app's rule

Back in the **Cursor Unofficial Android** app:

1. Go to **Settings → Chats & threads → Agent rule**.
2. Choose **Don't use a rule**.
3. Confirm on the pop-up.

Done. New agents now read the rule from your Cursor account, and the app sends nothing extra —
zero added tokens per spinup.

---

## Keeping it up to date

If `RULE.md` here changes and you want the update, repeat steps 1–3: copy the new text and replace
what you pasted in your User Rules. The app won't do this for you in this mode (that's the trade for
zero tokens).

## Prefer not to use the desktop app?

If you'd rather not touch desktop User Rules, just leave the app on **Use the default rule (this
repo)**, or point it at your own file with **Use my own rule**. Both work; they just add the rule's
tokens to each agent's first message.
