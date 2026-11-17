# voice-ai-prompting

A Claude Code skill for writing, reviewing, and debugging prompts for the Bigly
Sales Voice AI platform — outbound and inbound phone scripts that qualify leads,
transfer to a live agent, or schedule appointments.

## Install

Clone directly into your Claude Code skills directory. The repository *is* the
skill — no build or copy step.

```bash
git clone https://github.com/Bigly-Sales/voice-ai-prompting.git ~/.claude/skills/voice-ai-prompting
```

On Windows (PowerShell):

```powershell
git clone https://github.com/Bigly-Sales/voice-ai-prompting.git "$env:USERPROFILE\.claude\skills\voice-ai-prompting"
```

Restart Claude Code. Verify with `/skills` — `voice-ai-prompting` should be listed.

To pick up changes: `git pull` in that directory. `main` can be ahead of the last
release; to stay on a released version, check out its tag, for example
`git checkout v0.1.0`.

## Releases

A release is a tag `vX.Y.Z` on `main` with a GitHub release next to it. The tag is the
version; no file in the repository holds it. The plugin in `biglysales-claude-plugins`
takes the latest release, so a merged change reaches plugin users only after a release.

To cut one: **Actions → release → Run workflow** on `main`, and pick what to raise:

- `patch` — wording fixes, a new example, a clearer rule.
- `minor` — a new rule or reference file, or a rule that changes what the bot does.
- `major` — the skill is reorganized, or prompts written with the old version need a rewrite.

The workflow tags the current `main`, and writes the release notes from the pull
requests merged since the last release. It fails when `main` has nothing new.

## Layout

```
SKILL.md                              core conventions — loaded whenever the skill triggers
GAPS.md                               what the skill does not yet document (contributor doc)
references/
  platform-mcp.md                     MCP tool surface, write handshake, intro tags
  architecture.md                     component responsibilities, prompting limits, caching
  defaults.md                         default config tables and opening sentences
  global-rules.md                     verbatim Voice Prompt rule blocks
  variables.md                        standard {} variable set and injection points
  ooo-and-callback.md                 Out of Office and scheduled callback templates
  speech-to-speech.md                 S2S Intros: rules, delegation prompt, cascade conversion
  s2s-templates.md                    S2S Intro body, delegation prompt and tool row templates
  examples/                           anonymized production scripts, indexed in README.md
```

`SKILL.md` is loaded in full every time the skill activates, so it holds only what
applies to every script. Everything in `references/` is read on demand. Keep it
that way — moving reference material into `SKILL.md` costs tokens on every call.

## Contributing

- **New rule or convention** → `SKILL.md` if it applies to every script, otherwise
  the relevant `references/` file.
- **New example** → follow `references/examples/README.md` and add the index row.
- **New default value** → `references/defaults.md`.

Commit one logical change at a time so `git log` stays a readable history of how
the conventions evolved.
