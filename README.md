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

Press Enter at the greeting and choose any chapter:

- What a box is and where your copied source lives.
- Open a real shell and make a harmless workspace change.
- Try the console's tools picker; host editors are optional.
- Request a disposable demo credential, then approve or deny in the host inbox.
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
Denying or skipping works too. Press Enter to return to the menu and check later.
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
shell for recovery. The script uses the Linux platform's Bash and
`discobox-access`, without another toolchain or remote demo service.
