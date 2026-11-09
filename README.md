# Take a tour of Discobox

Run this on your host with a Discobox version supporting repository pre-harness scripts:

```sh
discobox run discobox-ai/tour
```

Choose your default harness if prompted. The tour runs in the Linux box before
that harness starts, from macOS, Linux or Windows hosts. First-use downloads
can take a few minutes. No agent account is required to try the menu; continuing
into your chosen agent can require its normal sign-in. Choose the shell harness
if you want to explore without an agent.

The tour is a full-screen terminal app in the Discobox look: the chapter list on
the left, the open chapter on the right. Use the mouse (click a chapter or a
button, scroll a long chapter) or the keyboard (arrows to choose, Enter to open
and press, Tab between buttons, Esc back to the list, 1–9 to jump to those chapters, c to
continue, q to exit). On a window narrower than 78 columns it shows one pane at
a time. Press Enter or click **Begin the tour** at the greeting and choose any
chapter:

- What a box is and where your copied source lives.
- The window: the `ctrl+a` leader key, clicking anything, and the `ctrl+a .`
  palette of every action.
- Open a real shell and make a harmless workspace change.
- Bring up the full console (`ctrl+a .` then `l`), the list of all your boxes.
- Try the console's tools picker; host editors are optional.
- SSH into the box, and use it as a Git remote (`ssh://BOX/...`, also shown in
  the tools picker) to fetch its commits on your host.
- Start a small website in the box and open it from your host: attached, the
  port is forwarded on its own (see the **Ports** link); detached, run
  `discobox proxy`. The website keeps running until you stop it from the
  chapter, with `kill "$(cat ~/.local/state/discobox-tour/site.pid)"`, or the box
  stops.
- Open the box's desktop at `localhost:6900`, when the box has one.
- Request a disposable demo credential, then approve or deny in the host inbox.
- Make a few harmless HTTP requests and find them in the audit view (`ctrl+a A`).
- Learn about harness setup and reviewing saved settings.
- Detach, reconnect, stop, restart and clean up.

The checkmarks show chapters you visited during this menu session. No chapter
or approval is required to finish. **Continue to my harness** records completion
in `~/.local/state/discobox-tour/completed` and starts the selected harness.
Further primary launches in this box skip the tour. A new box gets a fresh tour.

**Exit tour** or Ctrl-C returns to the primary shell without starting the
harness. EOF also exits without completion. To replay, open a shell in this
checkout and run:

```sh
.discobox/scripts/pre-harness --replay
```

Replay returns to that shell; it does not start another harness. To run it from
another directory, use the entry point's absolute path.

The access chapter asks only for `GET tour.discobox.invalid/demo`, with no
delegation. If approving, create/select a credential named `discobox-tour`
with the disposable value `tour-example-only`, never a production token.
No network request sends this value, and the script never prints a credential.
Denying or skipping works too. Choose **Check the request** now or later.
Ctrl-C exits the tour without starting a harness. Requester cancellation is
unsupported, so deny a pending request in the host inbox. Reopening the chapter checks the same request during that menu session.

Detach with Ctrl-A then d; return with `discobox attach BOX` on your host.
After collecting any work, archive with `discobox rm BOX`. This tour never
stops or archives the box automatically.

## How it starts

The executable `.discobox/scripts/pre-harness` runs automatically as the box
user on each actual primary terminal launch, before the harness. This is source
code running inside the sandbox, with its ordinary credential bindings. Extra
shells and tools bypass it; reconnecting to an existing terminal does not rerun
it. A failing or interrupted entry point prevents harness launch and leaves a
shell for recovery. The script is plain Bash with `discobox-access`. Two chapters
reach for tools the box image carries, only when you press their button: the
audit chapter uses `curl` for its four requests to `example.com` and `iana.org`,
and the ports chapter serves its website with `python3`.
