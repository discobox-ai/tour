# Discobox tour

A hands-on tour of the Discobox interface and what a box can do: the window
and its leader key, shells, the console, tools, SSH and Git, ports, the
desktop, secrets, the audit, and harnesses.

## Run it

From your host:

```sh
discobox run discobox-ai/tour
```

The tour opens full screen before your harness starts. Use the mouse or the
keyboard and take the chapters in any order. The tour itself needs no agent
account; continuing into an agent may ask you to sign in (the shell harness
needs none).

## Leave it

After **Begin the tour**, the chapter list ends with two entries:

- **Continue to my harness** (or press `c`) starts your harness. Later
  launches of this box skip the tour.
- **Exit tour** (or press `q`, or Ctrl-C at any time) leaves you at a shell
  without starting your harness. The tour shows again on the next launch.

## Replay it

From a shell in the box:

```sh
.discobox/scripts/pre-harness --replay
```

## Come back

Press Ctrl-A, then `d`, to detach; the box keeps running. Reattach from your
host:

```sh
discobox attach BOX
```

## Clean up

Once you have collected anything you want from the box, archive it from your
host:

```sh
discobox rm BOX
```

`BOX` is the box's name or ID; `discobox ls` lists them.
