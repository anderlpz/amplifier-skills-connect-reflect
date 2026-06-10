# Amplifier Skills Team

Shared Amplifier skills for the team.

This repository contains reusable Amplifier skills that can be installed and used by any team member using Amplifier.

## Available Skills

### `connect-reflect`

Guided Microsoft Connect performance review reflection. Mines project history, sessions, meetings, and transcripts across all evidence sources, then walks you through a month-by-month "memory lane" to capture the real stories behind the work.

**Use when:**
- It's Connect time
- You need to fill out your performance review
- You want to reflect on impact and accomplishments in your voice

**Key features:**
- Mines git history (authorship-verified)
- Extracts Amplifier session summaries
- Scans meeting transcripts
- Finds voice transcripts
- Walks you through memory lane interactively
- Produces paste-ready answers in your voice

## Installation

Add this to your `~/.amplifier/settings.yaml`:

```yaml
skills:
  dirs:
    - git+https://github.com/anderlpz/amplifier-skills-team@main#subdirectory=skills
```

Then restart Amplifier or clear the skill cache. On your next session, the skills will be available.

**To use a skill:** Start a new Amplifier session and type `/skill-name`, e.g. `/connect-reflect`

## Contributing New Skills

To add a new skill to this repo:

1. Create a new directory under `skills/` with your skill name: `skills/my-skill/`
2. Write your `SKILL.md` file following the [Amplifier SKILL.md specification](https://github.com/microsoft/amplifier)
3. Test it locally in `~/.amplifier/skills/my-skill/` first
4. Commit to a feature branch and open a PR
5. Once merged, it's available to everyone on the next cache clear

## License

These skills are shared with the team for collaborative use.
