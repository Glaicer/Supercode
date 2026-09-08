# Supercode

I spend most of my day inside OpenCode, so I started fixing the small things to make it more convinient. Then those fixes turned into this — a little shelf of tools I actually use every day.

Every plugin here started as a personal itch, ships as its own tiny package, and lives in this repo as a git submodule.

## [Skill Commands](https://github.com/Glaicer/supercode-skill-commands)

Makes your skills show up in `/` autocomplete.

OpenCode *already* registers every skill as a command — `/my-skill` just works — but the TUI quietly hides them from the popup, so a skill is only reachable if you happen to remember its name. This plugin re-registers each skill as an ordinary command, mirroring OpenCode's own discovery walk (up to the worktree root, nearer shadows farther). A real command always wins over a skill of the same name, so there are no duplicates — just your skills, finally visible.

## [Plugin Updater](https://github.com/Glaicer/supercode-plugin-updater)

OpenCode caches npm plugins and managed tools (prettier, pyright, …) forever. Whatever version was current on first install stays there. The fix used to be deleting cache folders by hand, but this needs to be done regularly, or you need to set up a schedule. Of course, I would like something to notify me when a new version of the package is released.

This one checks once a day on startup, toasts you when something is stale, and `/plugin-updates` opens a review screen grouped into Plugins, Managed tools, and Skipped. Pick with Space, hit `U`, confirm — done on next restart.

## [Token Usage Panel](https://github.com/Glaicer/supercode-token-usage-panel)

See where the tokens went with detailed spending stats, cache rate, cost, and live token-per-second generation speed in a collapsible sidebar panel. 

The totals include the parent session and every level of subagents beneath it.

## [Session Recap](https://github.com/Glaicer/supercode-session-recap)

A collapsible recap in the session sidebar: after every turn, two sentences max on where things stand. For when you return to a session after lunch and past-you left no notes.

The recap is written by OpenCode's `small_model` — the same lightweight model that generates session titles — inside a throwaway child session that gets deleted afterwards. It costs almost nothing and leaves zero trace in your actual conversation.



## [Autoinvoke Skill Gate](https://github.com/Glaicer/supercode-autoinvoke-skill-gate)

Stops the model from auto-using your manual-only skills. Claude Code, Codex, and OpenCode v2 already have a way to mark a skill as "don't auto-invoke me" — OpenCode v1 just ignores it, so the model sees everything and may grab the wrong skill on its own. This one strips those manual-only skills from `<available_skills>`, cleaning up context and preventing surprise side effects. Nothing is blocked: `/my-skill` or "use my-skill" still works — it just never happens automatically.



> [!NOTE]
> More plugins are currently in development and will be shipped soon:
> - **auto-approval-reviewer**: a must-have feature of Codex and Claude Code that uses LLM to evaluate the security of commands before running them.
> - **goal-loop**: `/goal "<done-condition>"` keeps the agent working through idle until a judge verdict says it's met. A lot of harnesses has it already, but OpenCode doesn't.
> - **hashline-editing**: snapshot-guarded `read`/`edit` — patches apply by `[PATH#TAG]` and stale edits fail instead of clobbering.
> - **persistent-memory**: durable project `MEMORY.md` + per-session notes with FTS search via `memory.search`.
> - **review-agent**: read-only `@review` agent that checks Standards vs Spec and persists the verdict.

---

## Install

Each plugin is its own repo, included here as a submodule. Easiest path is per-plugin, from its own README:

```bash
opencode plugin <name> --global
```

