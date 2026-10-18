# Lecture notes builder

An AI skill that merges a lecture transcript and the lecture slides into one exam-ready note, filed in the right course folder of an Obsidian vault.

It works with any capable AI model. The skill is a plain Markdown prompt (`SKILL.md`) in the open Agent Skills format, so nothing in it is tied to one vendor.

## What it does

Transcripts carry the explanation but ramble. Slides carry the structure but say little. This skill walks the slides in order, pulls the matching stretch of transcript for each, keeps the lecturer's examples and anything they stressed, and drops the rest.

The note it writes has frontmatter, key takeaways, notes in lecture order, a definitions table, likely exam points and open questions. Skipped slides stay in the note and are marked "not covered in lecture". Anything the recording garbled is marked `[unclear in recording]` instead of guessed. It links back to the previous lecture, adds the note to the course index, and copies the naming and heading style the folder already uses.

## How it works

| Step | What happens |
|---|---|
| 1. Gather | Reads the transcript and the slides (text per slide, slide numbers kept). Works out the course, lecture number and topic from the slides or the recording title. |
| 2. Find the folder | Finds the course folder, reads one or two existing notes to match their style, and finds the previous lecture's note. Creates the folder and an index if there is none. |
| 3. Align | Pairs each slide with what was said about it. Notes anything said with no slide, and any slide that was skipped. |
| 4. Write | Fills the note template, or the folder's own format if it has one. |
| 5. File | Saves the note, adds it to the course index, links the previous lecture forward. |
| 6. Check | Confirms every slide is accounted for, every number and formula matches a source, and every link resolves. Reports where the note went and what it flagged. |

If only one of the two sources exists, it carries on with that one and says at the top of the note which is missing.

## Requirements

| Need | Why |
|---|---|
| An AI model that can read PDFs or PowerPoint, or the slide text pasted in | The slides are one of the two inputs |
| A transcript, from any recorder (Granola, Otter, Teams, Zoom, a phone app) | The other input |
| Read and write access to your notes folder, if you want the note filed for you | Steps 2 and 5 read existing notes and save the new one |
| Obsidian, optional | The note uses `[[wikilinks]]` and YAML frontmatter. Any Markdown folder works, but the links only resolve in Obsidian or a tool that reads them. |

No code, no API keys and no packages to install.

## Install

| Where you run it | How |
|---|---|
| An agent that reads skills folders (Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot, Cursor and the others listed at [agentskills.io](https://agentskills.io)) | Clone this repo into the agent's skills folder as `lecture-notes-builder`, for example `git clone https://github.com/Vidwaansinghania/Lecture-Notes-Builder.git ~/.claude/skills/lecture-notes-builder`. Each agent documents its own folder. The agent loads the skill when a request matches its description. |
| A chat assistant without skills (ChatGPT, Gemini, Claude.ai, a local model) | Paste everything in `SKILL.md` below the `---` header into custom instructions, a project, a Gem, or the first message. Attach the slides and transcript. You save the note yourself. |

## Using it

```
Write up today's Corporate Finance lecture. Slides are in Downloads/FIN2001_L6.pdf.
```

## Licence

Apache-2.0. See [LICENSE](LICENSE). Anyone who uses or builds on this work must keep the [NOTICE](NOTICE) file and credit Vidwaan Singhania.
