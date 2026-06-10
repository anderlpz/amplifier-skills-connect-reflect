# connect-reflect

A guided performance review reflection skill for [Amplifier](https://github.com/microsoft/amplifier).

Mines your project history, Amplifier sessions, meeting transcripts, and voice notes, then walks you through a month-by-month "memory lane" conversation to capture the real stories behind your work. Produces paste-ready answers in your voice.

The reflection is the product. The paste-ready answers are a side effect.

## What it does

1. Parses your review form structure (currently built for Microsoft Connect, adaptable to other formats)
2. Finds or builds a voice profile so the output sounds like you, not like AI
3. Mines evidence from multiple sources in parallel:
   - Git history across all your projects (authorship-verified)
   - Amplifier session summaries
   - Meeting transcripts
   - Voice transcripts and notes
   - Team tracking and org context
4. Walks you through a month-by-month reflection conversation
5. Synthesizes evidence and drafts answers in your voice
6. Final walk-through for review before producing the document

## Install

Add this line to your `~/.amplifier/settings.yaml`:

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

Or just say "help me with my Connect", "time for my performance review", or "I need to do my review."

## What makes this different

This skill was built from a real Connect session and encodes hard lessons:

- **Impact is what work enabled, not what was shipped.** No commit counts. No line counts. Impact is new thinking, scaled approaches, and influence on others.
- **Authorship is verified.** Every project is checked against git history. You don't take credit for work you didn't do.
- **Voice matters.** The skill loads or builds a voice profile so the output sounds like the person who wrote it. AI tells (em dashes, "robust framework", "enhanced capabilities") are actively avoided.
- **Honesty over bravado.** Where you haven't done something yet, the skill says so in plain language rather than faking expertise.
- **The conversation IS the product.** Automated mining is just a memory trigger. The real answers come from you engaging with evidence and telling the real story.

## Requirements

- [Amplifier](https://github.com/microsoft/amplifier) with the skills tool configured
- Projects in a workspace directory with git history
- Works best with Amplifier session history available

## Contributing

To improve this skill, edit `skills/connect-reflect/SKILL.md` and submit a PR.
