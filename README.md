# connect-reflect

A guided performance review reflection skill for [Amplifier](https://github.com/microsoft/amplifier).

## Why

Performance reviews don't capture what actually happened. You open the form, stare at it, and try to remember six months of work. The result is either a rushed list of things you shipped or an AI-generated wall of corporate language that doesn't sound like you.

The problem isn't the form. It's that the evidence of what you actually did is scattered across git repos, meeting transcripts, chat messages, session logs, planning docs, and your own memory. Nobody has time to mine all of that. So you write from whatever you remember in the moment, and the review undersells what happened.

This skill fixes that by doing two things:

1. **It mines the evidence for you.** Git history, Amplifier sessions, meeting transcripts, voice notes, team tracking. Authorship-verified so you don't accidentally claim someone else's work. Automated, parallel, runs in minutes.

2. **It walks you through a guided reflection.** Not a form-filling exercise. A conversation where the evidence triggers your memory and you tell the real story. What mattered. What was hard. What you learned. What happened in meetings and conversations that never shows up in a commit log. The corrections you make during this conversation are the most valuable output of the entire process.

The paste-ready review answers are a side effect of genuinely reflecting. That's the point.

## How it works

1. **Understand the form** — Parses your review structure (built for Microsoft Connect, adaptable to other formats)
2. **Find or build a voice profile** — Loads your writing patterns so the output sounds like you, or builds one from your sessions and writing samples
3. **Mine evidence** — Parallel agents scan git history, Amplifier sessions, meeting transcripts, voice notes, and team tracking
4. **Guided reflection** — Walks through your review period, surfacing evidence and asking what it meant. Adapts to how your work naturally clusters: by project, by theme, by phase, whatever fits. You tell the real story.
5. **Synthesize** — Maps your reflections to the review form fields
6. **Draft answers** — Writes in your voice, not AI voice
7. **Final review** — Walk-through with you before producing the final document

## Install

Requires [Amplifier](https://github.com/microsoft/amplifier) with the skills tool configured.

Add this line to `~/.amplifier/settings.yaml`:

```yaml
skills:
  dirs:
    - git+https://github.com/anderlpz/amplifier-skills-connect-reflect@main#subdirectory=skills
```

Start a new Amplifier session. The skill is available immediately.

## Use

```
/connect-reflect
```

Or just say "help me with my review", "Connect is due", or "I need to do my performance review."

## What it gets right

This skill was built from a real review session and encodes hard lessons:

- **Impact is what work enabled, not what was shipped.** No commit counts. Impact is new thinking, scaled approaches, and influence on others.
- **Authorship is verified.** Every project is checked. You don't take credit for work you didn't do.
- **Voice matters.** The output sounds like you. AI tells (em dashes, "robust framework", "enhanced capabilities") are actively avoided.
- **Honesty over bravado.** Where you haven't done something yet, it says so in plain language.
- **The conversation is the product.** Mining is a memory trigger. The real answers come from you engaging with evidence and telling the real story. The things that matter most in a review — the meeting that changed your thinking, the challenge you grew from, the collaboration that doesn't show up in git — only come from you.

## For Microsoft employees

The skill is built with the Microsoft Connect review structure in mind and checks for org-published guidance (Security Activation Examples, D&I frameworks, SFI alignment, etc.) to make sure your language fits what Microsoft expects to see. It handles the full Connect form: core priorities, impact narrative, D&I, Security, challenge/setback, future priorities, growth opportunities, and conversation starters.

## Contributing

To improve this skill, edit `skills/connect-reflect/SKILL.md` and submit a PR.
