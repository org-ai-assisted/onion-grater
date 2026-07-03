# Agent Instructions for onion-grater

## Project Overview

onion-grater is a whitelisting filter for the Tor control protocol. It acts
as a proxy between a client application (on an Anonymity Distribution
Workstation) and Tor, allowing only control commands that are safe for
anonymity and blocking dangerous ones. Per-application whitelists ("profiles")
match a command's entire argument string as an anchored regex.

- Upstream repo: Whonix/onion-grater
- Language: Python
- Profiles: `usr/share/doc/onion-grater-merger/examples/`
- Filter: `usr/lib/onion-grater`

## Tests

This package has no in-tree test suite. Its comprehensive tests -- profile
regression / reproduction tests, adversarial control-command probes, and a
full-stack end-to-end suite (a throwaway offline tor plus the real
onion-grater over a veth network) -- are too high-volume for human review and
live in the AI-maintained dist-ai repo, not here:

  https://github.com/org-ai-assisted/dist-ai -> usr/share/onion-grater-tests/

Run them against this checkout:

    ONION_GRATER_REPO="$PWD" onion-grater-tests       # in-process unit / reproduction
    ONION_GRATER_REPO="$PWD" onion-grater-tests-e2e   # full-stack (needs tor + sudo)

`ONION_GRATER_REPO` points the suite at this checkout's `usr/lib/onion-grater`
and its example profiles. A behavior change here -- a profile edit, a matcher
or rewriter change -- may require updating that suite.
