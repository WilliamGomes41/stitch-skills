# William's Stitch skills fork

Upstream: [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills).
This fork is a shared plugin source. It does not depend on a chat or on the Metis
application repository. Upstream licenses and plugin files remain unchanged.

## Install in your own Codex environment

Run these commands in the environment where you actually use Codex. This can be
your computer or a managed agent environment. Requires Codex with `plugin`
support, Git and network access.

```sh
codex plugin marketplace add WilliamGomes41/stitch-skills --ref main
codex plugin add stitch-design@stitch-skills
codex plugin add stitch-utilities@stitch-skills
codex plugin list --marketplace stitch-skills
```

`stitch-utilities` provides the `design-md` dependency used by the design workflow.
`stitch-build` is optional and is not needed for Metis's existing Python-rendered
HTML/CSS console. Reload plugins or start a new Codex session after installation.

If `stitch-skills` already refers to the original Google repository, first run
`codex plugin marketplace remove stitch-skills`, then run the commands above.
This replaces that marketplace source; it does not delete any remote repository.

In Codex's plugin marketplace settings, the equivalent source is
`https://github.com/WilliamGomes41/stitch-skills`, with Git ref `main`.
Other agents can use the upstream README's host-specific instructions with this
fork as their source. A fork alone does not install a plugin on anyone's computer.

## Enable periodic updates once

GitHub may disable Actions in a newly created fork. Open
[Actions](https://github.com/WilliamGomes41/stitch-skills/actions) and enable
workflows if GitHub prompts you. In **Settings → Actions → General → Workflow
permissions**, enable **Allow GitHub Actions to create and approve pull requests**.
The workflow uses PR creation only; it neither approves nor merges PRs.

The `Check upstream updates` workflow runs each Monday at 06:20 UTC and can also
be started with **Run workflow**. It compares the fork with upstream `main` and
opens one update PR if needed. An existing open update PR is reused and tracks
further upstream commits. Review changes before merging; local fork changes are
preserved and merge conflicts require review. A green run with no PR means there
were no new upstream commits. GitHub can delay scheduled runs or disable schedules
after 60 days of inactivity in a public repository; check Actions if updates stop.

After merging an update, refresh each installed environment:

```sh
codex plugin marketplace upgrade stitch-skills
codex plugin add stitch-design@stitch-skills
codex plugin add stitch-utilities@stitch-skills
codex plugin list --marketplace stitch-skills
```

## Stitch connection is separate

The plugins supply skills. Generating and editing designs additionally requires
the [Stitch MCP connection](https://stitch.withgoogle.com/docs/mcp/setup/) and
your own account access. Configure credentials in your agent environment, never
in this fork or in Metis. Verify the connection with a synthetic design before
claiming it works. Installation is not evidence of an authenticated connection.
