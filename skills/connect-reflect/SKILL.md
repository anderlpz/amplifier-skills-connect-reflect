---
name: connect-reflect
description: >
  Guided Microsoft Connect performance review reflection. Mines project history,
  sessions, meetings, and transcripts across all evidence sources, then walks you
  through a month-by-month "memory lane" to capture the real stories behind the
  work. Produces paste-ready Connect answers in your voice. Use when it's Connect
  time, "help me with my Connect", "time for my performance review", "Connect is
  due", or "I need to do my review."
user-invocable: true
allowed-tools:
  - read_file
  - write_file
  - edit_file
  - bash
  - glob
  - grep
  - delegate
  - web_fetch
  - load_skill
  - todo
model_role: writing
---

# Connect Reflect

A guided performance review process that treats the act of reflecting as the
real product, not just the output document. The Connect answers are a side
effect of genuinely walking through what you did, what it meant, and what
you learned.

## Inputs

- `<connect_url>`: (Optional) URL to the Connect form or a PDF/screenshot of it.
  If not provided, the skill will ask what questions need answering.
- `<period>`: (Optional) The review period, e.g. "Nov 2024 - June 2026".
  If not provided, will ask.

## Hard Rules

These are non-negotiable. Every one came from a real correction during a
real Connect session.

1. **Impact is what the work ENABLED, not what was shipped.** Never count
   commits, lines of code, or PRs as impact. Impact is new thinking, scaled
   approaches, novel capabilities, and influence on others.

2. **Verify authorship on everything.** Before including any project, run
   `git log --format='%an' | sort | uniq -c | sort -rn` and confirm the
   user is a significant author. Don't take credit for others' work.

3. **Match the user's voice.** Load or build a voice profile (Step 2).
   The Connect should sound like the person wrote it. Watch for AI tells:
   em dashes, "robust framework", "enhanced capabilities", "increasing rigor",
   "architectural layer", and other corporate/AI phrasing.

4. **Be honest about gaps.** Where the user hasn't done something yet or
   doesn't have deep expertise, say so in plain language. "I want to learn
   more about..." beats false confidence every time.

5. **The reflection IS the product.** Mining is just a memory trigger. The
   real answers come from the user engaging with evidence and saying "no,
   the real story is..." Every correction is the most valuable signal.

6. **Align with current org expectations.** Check for any company-published
   Connect guidance, activation examples, or frameworks and align framing
   accordingly. Don't be prescriptive about specific frameworks, just make
   sure the language fits what the org expects to see.

7. **Paste-ready output.** The final document mirrors the Connect form
   exactly. No markdown formatting in the paste text. No bold, no bullets.
   Just clean paragraphs the user can copy into form fields.

## Steps

### 1. Understand the Connect Form

Figure out what needs to be filled in. Either:
- Fetch and parse a Connect URL/PDF the user provides
- Ask the user to describe or paste the form structure
- Use the standard Microsoft Connect structure as a baseline

Identify every field that needs an answer. Map the form structure so the
final output mirrors it exactly.

Also ask: "Did you change teams or managers during this period?" If yes,
the Connect may need to cover multiple eras. This is an edge case but it
changes the structure significantly.

**Success criteria**: Clear list of every Connect field that needs content,
in the order they appear in the form.

### 2. Find or Build a Voice Profile

Look for an existing voice profile:
- Check `~/.amplifier/profiles/` and project-level `.amplifier/profiles/`
- Look for files named after the user or containing "voice", "profile",
  "tone", "style"

If a voice profile exists, load it and confirm with the user.

If no profile exists, ask: "I don't have a voice profile for you yet.
Want me to build one from your sessions and writing? It'll help the
Connect sound like you, not like AI."

If yes, build a profile by:
- Mining recent Amplifier sessions for natural phrasing patterns
- Reading writing samples (messages, docs, blog posts)
- Noting: sentence starters, hedging language, vocabulary, characteristic
  phrases, what they NEVER say
- Save to `~/.amplifier/profiles/<name>.md` for future use

**Success criteria**: A voice profile is loaded or built, and the user
confirms it represents how they write.

### 3. Gather Evidence (automated, parallel)

Mine ALL available evidence sources in parallel. Commits are just one
signal. The meta-work (meetings, conversations, teaching, mentoring,
thinking) is often where the real impact lives, especially for non-engineering
roles like design architects.

Dispatch agents in parallel, one per source:

**3a. Git history**
- Scan all projects in the user's workspace (ask for the path if not obvious)
- `git log --oneline --since=<start> --until=<end>` for each repo
- Verify authorship on every repo
- Cluster repos by theme
- Execution: Delegate to self or foundation:explorer, one per cluster

**3b. Amplifier sessions**
- Find session directories across all projects
  (`~/.amplifier/projects/` has per-project session stores)
- Extract session metadata: topics, dates, what was worked on
- Group by month and project
- Execution: Delegate to foundation:session-analyst

**3c. Meeting transcripts**
- Search for meeting transcript files (.md, .txt) across projects
- Check Inbox/, Documents/, Recordings/, Downloads/
- Look for Teams transcript markdown files (from the Teams Transcript
  MD browser extension or similar tools)
- If the user has access to Teams/M365 transcript APIs, use those
- Extract: who was involved, what was discussed, key themes
- Execution: Delegate to self or foundation:explorer

**3d. Voice transcripts and notes**
- Search for voice transcript files (SuperWhisper, Otter, or similar)
- Check planning, growth, and learning repos for reflection notes
- Check for raw voice capture files (often in .amplifier/profiles/)
- Execution: Delegate to foundation:explorer

**3e. Team tracking and org context**
- Check for Team Pulse data, initiative assignments
- Look for formal role assignments, charter documents
- Search for org-published Connect guidance (security activation
  examples, D&I activation examples, etc.)
- Execution: Delegate to foundation:explorer

**Rules for this step:**
- Every git cluster must have authorship verified before inclusion
- Remove repos where the user isn't a significant author
- Remove repos with 0 commits in the review period
- Don't count commits as impact, just use them to identify what was
  worked on. The actual impact comes from the user's reflection in Step 4.

**Success criteria**: Evidence gathered from all available sources.
Organized by month and theme. Authorship verified. Non-authored repos
excluded.

### 4. Walk Down Memory Lane (interactive)

This is the most important step. Present the evidence as a timeline
and have a CONVERSATION about each period. The mining was just the
setup. This is where the Connect actually gets written.

For each month or phase:
1. Show what the evidence says happened: "In October, I see you were
   deep in [project]. There were sessions about [topic], a meeting
   with [person], and you were building [feature]."
2. Ask open questions:
   - "What was going on during this time?"
   - "What mattered most?"
   - "What was hard? What did you learn?"
   - "Did anything happen that doesn't show up in the evidence?
     Conversations, decisions, things you influenced?"
3. Listen for the real story. The user will correct you, add context,
   reframe. CAPTURE THEIR WORDS.
4. Ask specifically about:
   - Work that happened in meetings, not in code
   - People they helped or mentored
   - Challenges and what they learned from them
   - Security and privacy thinking (even small decisions count)
   - Inclusive design or D&I contributions
   - Things they started that others finished, or vice versa

If the user mentions a meeting or conversation that was important,
ask if there's a transcript or recording available. If so, fetch and
mine it during the conversation.

**Rules:**
- Don't rush. This is a reflection, not a form-filling exercise.
- Present evidence in digestible chunks, not a data dump.
- If the user says "that's not mine" or "remove that", do it instantly.
- The user's corrections are the most valuable output of this step.
- Capture the user's exact phrasing for key stories.

**Success criteria**: The user has walked through the full review period
and feels like they've genuinely reflected. Key stories captured for
each Connect section.

### 5. Synthesize Evidence Map

Produce an evidence map connecting the user's reflections to Connect
fields:
- Proposed core priorities (based on what they did, in their words)
- Impact evidence per priority
- D&I evidence
- Security evidence
- Challenge/growth evidence
- Forward-looking priorities
- Growth opportunities

Present to the user: "Does this feel right? Did I miss anything?"

**Success criteria**: Evidence map reviewed and approved by the user.

### 6. Draft Answers

Write the Connect answers using:
- The user's voice profile for tone
- The evidence map for content
- The Connect form structure for organization
- The user's own words from the reflection

**Rules for drafting:**
- First person throughout
- Match the user's natural voice
- Past tense for Reflect, future for Plan
- No em dashes
- No jargon the user wouldn't naturally use
- Where the user expressed uncertainty, preserve that honesty
- Plain text paragraphs, no markdown formatting in answer text
- Structure the output file to mirror the Connect form exactly

**Success criteria**: Complete draft with every Connect field populated,
in the user's voice.

### 7. Final Walk-Through (interactive) [human]

Present the draft section by section:
- "Does this sound like you?"
- "Anything to change?"
- Make edits on the spot

Watch for:
- AI voice leaking through (em dashes, corporate phrasing)
- Claims that overstate what the user did
- Forward-looking sections that sound like engineering manifestos
  instead of honest growth goals
- Would the user be comfortable reading this to their manager?

**Success criteria**: User has reviewed every section and confirmed
they're ready to paste.

### 8. Produce Final Document

Write the paste-ready Connect answers to a file.

Also save as companion files:
- Evidence map (useful for future Connects)
- Reflection notes (the raw stories and corrections from Step 4)
- Voice profile (if one was built in Step 2)

Tell the user: "Your Connect answers are at [path]. Open the file,
each section is labeled with the Connect form field. Copy the text
under each label and paste it in."

Remind them: "I also saved your evidence map and reflection notes.
These are useful for your next Connect. The record of impact builds
over time."

**Success criteria**: Final document saved. User knows where it is
and how to use it. Evidence and reflection preserved for next time.
