# Cursor Unofficial Android — Agent Rule

Apply this whenever the user is chatting with you from the **Cursor Unofficial Android** phone app
(`com.cursorandroid.app`). It tells you how to interact with everything that app can send you and
everything it can receive back.

## What this app is

An unofficial Android remote control and inbox for Cursor Cloud Agents (and the user's machines and
pools). **The phone does not run the agent** — your work runs on Cursor cloud VMs or the user's
machines. Assume the user is often on their phone, not at a desktop: keep replies phone-friendly and
self-contained, and don't assume they can open desktop-only paths or tools.

## What the app can SEND you

### Text in the prompt
Anything the user types, pastes, or that the app inlines goes into `prompt.text`. Treat all of it as
part of your instructions and read it carefully. There is **no separate arbitrary file upload** on
the Cloud Agents API — the only inputs are `prompt.text` and `prompt.images`. If the user refers to
"the file I sent," look for it inlined in the prompt text or as an attached image.

### Images (vision)
The user can attach photos or images. They arrive as prompt images: either base64 `data` +
`mimeType`, or an `http(s)` `url` the API fetches. Limits: up to **5 images, 15 MB each**, formats
`image/png`, `image/jpeg`, `image/gif`, `image/webp` (HEIC may be converted on the phone before
sending). When an image matters to the task, say what you actually see in it.

### Target of a new agent
When the user starts a new agent from the phone, it can target a repo, a saved environment, a
machine, a pool, or **no repo at all** — the user picks on the phone. Don't assume a repo is present;
a no-repo run is normal and means "start from scratch / no checkout."

### MCP
MCP servers may be attached from the phone at agent-create time. Don't assume MCP is desktop-only —
use whatever tools are attached to this run.

## What you can SEND BACK to the app

### Files / artifacts (critical)
When you produce a file the user should open or keep on the phone:
1. Save it under workspace **artifacts** (use the paths from List Artifacts, e.g.
   `artifacts/report.pdf`).
2. In your final reply, name that path and tell them they can tap **Open** or **Save** on the phone.
3. Prefer artifacts over dumping huge content only into chat text. **Never rely on desktop-only
   paths** — the phone can't reach them.

On the phone this shows as: the latest artifact card (Open + Save), a short Artifacts history,
**Open** = a signed HTTPS URL (valid ~15 min), **Save** = downloads to the phone via Download
Manager.

### Pictures / video back
Prefer artifacts (`artifacts/demo.mp4`, `artifacts/ui.png`) so Open/Save work on the phone, and also
describe what they show. Don't assume a desktop preview.

### Pull requests
If you open a PR, include the full `https` PR URL in the git/result metadata. The phone can then
offer **Open PR** and can filter agents by `prUrl`.

### Replies
Always write a real, user-visible answer in your reply, even though the phone also shows thinking and
tool-call UI. Keep it phone-readable: short paragraphs, no giant walls of text, no reliance on the
user scrolling a desktop.

## Chat / run behavior

- **Follow-ups queue.** Messages the user sends from the phone while a run is active queue up and
  become the **next run** (`POST …/runs`) when the current one finishes. Do not assume you can be
  steered mid-run — the public API has no mid-run steer.
- **Send immediately.** The user can tap **Send immediately** on a queued message. That **cancels
  the active run** (`POST …/cancel`) and sends their follow-up as a new run. Treat a
  cancel-then-new-run as intentional, not an error — pick up the new instruction.
- Finish cleanly so the queued follow-up (if any) starts from a good state.

## Scope

This rule is about **Android-app interaction only**: artifacts, images, prompt text, and phone chat
behavior. It doesn't change how you write code or make technical decisions — it only shapes how you
send things to and receive things from the phone. If set as a Cursor account **User Rule**, keep
**Always Apply** on so it applies to every cloud, machine, and pool agent.
