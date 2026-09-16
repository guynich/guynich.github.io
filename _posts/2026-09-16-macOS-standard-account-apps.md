---
layout: post
title: "A standard macOS account install for sandboxing agents and local LLM tools"
date: 2026-09-16
---

Sandboxing AI applications has become a recurring theme lately. Agents that
can read files, hit the network, and call out to other tools are a different
risk profile than a chat window, and a lot of recent discussion has been
about how to contain that. Containers and VMs are the usual answers, but on
a Mac there's a lighter option that's easy to overlook: a second, standard
(non-admin) user account.

## Why a standard account

A standard macOS account can't install privileged software, can't modify
system files outside its own home directory, and can't grant itself new
permissions. All are good properties for something running agentic or
LLM-adjacent tooling you don't fully trust. Unlike a container or VM, it
still has direct access to the Mac's full compute: GPU, unified memory, disk
with nothing virtualized, nothing partitioned off. For local inference
workloads in particular, that matters; you don't want to be sandboxing your
way into losing half your throughput.

I use this pattern for my own agent setup: an admin account for normal use,
and a separate standard account where agent and local-LLM tooling actually
run.  The admin account hosts a web proxy for further isolation.  I wrote about
this in July for
[local coding agent](https://github.com/guynich/local-coding-agent) work.

## The catch: most apps assume they're admin

The problem is that AI app installers are almost never written with a
standard-account install in mind. They assume they can use root privileges
to write to `/Applications`, register a privileged helper, or open firewall
ports. All these are things a standard account can't do on its own. So "just
create a second account" only gets you partway; you're often stuck reverse-engineering what the installer needed admin for, and whether it's load-bearing once it's gone.

NVIDIA's [PAIR](https://github.com/NVIDIA/Personal-AI-Router), a router
that distributes local inference across machines on your home network, is
a good recent example. I wanted it running in the standard account rather
than alongside my normal admin session, and it turned out to work, with one
admin-side cleanup step. I wrote it up as a
[GitHub discussion](https://github.com/NVIDIA/Personal-AI-Router/discussions/89)
on the project; the short version:

- Install into `~/Applications` in the standard account, not
  `/Applications`.
- PAIR's installer registers a privileged helper
  (`com.nvidia.nvpair.helper`) that manages its firewall rules - a standard
  account can't approve that itself, so this needs a one-time trip through
  an admin account to unregister it (`launchctl bootout`, then remove the
  LaunchDaemon and the helper binary).
- With the helper gone, the firewall rules it would have opened need to be
  added manually.
- After that, everything - node discovery, pairing, inference through the
  proxy - ran with no root processes at all.

The GitHub discussion has more context.

## My ask

My request to AI app developers, PAIR included: offer a
**standard-account install** path as a first-class option, not something a user
has to reverse-engineer.

Practically that means documenting (or better, not
requiring) whatever admin step the installer currently assumes - privileged
helpers, firewall rules, `/Applications` writes. For tools that are increasingly
being pointed at agentic workloads, "runs fine as a standard user" is a
reasonable bar, and one most installers aren't meeting yet.
