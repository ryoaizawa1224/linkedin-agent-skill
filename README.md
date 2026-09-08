# The LinkedIn agent skill for Codex

Eleven Codex skills for running the writing and planning side of a LinkedIn account. Free, MIT, no signup, no API key, nothing to connect.

One writes posts from 21 hook formulas. One comments on other people's posts. One handles replies under yours. One scores your profile out of 100 and rewrites what lost points. One plans the week: what to post, when, and who to engage with.

And one is the humanizer. It strips em dashes, stock AI phrasing and invisible format characters out of a draft, then scores what is left against a five-check local heuristic panel before you see it.

**Nothing gets posted until you say yes.** These skills write. You post.

This fork ports Jake Schincariol's original Claude skill pack to OpenAI Codex. The content strategy and Python tooling remain his work; the Codex packaging and invocation conventions are adapted here.

## Install

### Ask Codex to install from GitHub

Give Codex this repository and ask it to install all skills under `skills/`:

```text
https://github.com/ryoaizawa1224/linkedin-agent-skill

Install the LinkedIn skills in this repository, then confirm $li-post is available.
```

Codex's skill installer supports installing skills directly from a GitHub repository into `$CODEX_HOME/skills` (normally `~/.codex/skills`).

### Manual global install

```bash
git clone https://github.com/ryoaizawa1224/linkedin-agent-skill.git
mkdir -p ~/.codex/skills
cp -r linkedin-agent-skill/skills/li-* ~/.codex/skills/
```

### Project-local install

Copy the skill folders into your repo's `.agents/skills/` directory:

```bash
mkdir -p .agents/skills
cp -r /path/to/linkedin-agent-skill/skills/li-* .agents/skills/
```

The repository also includes `.codex-plugin/plugin.json` for Codex plugin packaging.

## Set up your voice

Spend ten minutes on `templates/voice.md`. Copy it to:

```text
~/.codex/linkedin/voice.md
```

Fill it in, or give Codex three of your own past posts and ask it to write the voice profile from them. Every relevant skill reads that local file.

Keep `voice.md`, `log.md` and `plan.md` local. Do not commit them to this public repository if they contain personal or private information.

## The eleven

| skill | what it does |
| --- | --- |
| `$li-post` | One idea into a post. Three hook options from [21 formulas](skills/li-post/hooks.json), one full draft, humanized before you see it. |
| `$li-comment` | Comments on other people's posts. Nine types, picked by what the post actually is. Never "Great post!". |
| `$li-reply` | The thread under your own post. Sorts comments into lead / substance / peer / support / noise, then writes in that order. |
| `$li-profile` | Scores your profile against a [12-part rubric](skills/li-profile/rubric.json) out of 100, then rewrites in fix-first order. |
| `$li-plan` | The week. What to post, when to post it, and the 10 people to engage with. Writes `~/.codex/linkedin/plan.md`. |
| `$li-human` | The humanizer. Two local Python scripts. |
| `$li-carousel` | Document posts. Slide-by-slide copy, cover, and PDF plan. |
| `$li-repurpose` | One video, newsletter or transcript into a week of posts that each stand alone. |
| `$li-dm` | The 200-character invite note, first message, and two follow-ups. |
| `$li-inbox` | Triages the inbox into lead / recruiter / peer / ask / spam. |
| `$li-audit` | Post-mortem on what you have published. Ranks by engagement rate and reach multiple, not impressions. |

## The humanizer

`$li-human` ships two Python scripts with no external dependencies. They run locally on your text.

```bash
python3 humanize.py draft.txt --report
python3 detect.py draft.txt
python3 detect.py before.txt after.txt
```

It automatically handles:

- Invisible and format characters such as zero-width spaces, joiners, soft hyphens, BOMs and non-breaking spaces.
- Typography such as em dash -> comma, en dash -> hyphen, curly quotes -> straight quotes and ellipsis -> three dots.
- A lexicon of stock AI phrasing in [`slop.json`](skills/li-human/slop.json).

Structural tells such as rule-of-three phrasing, rhetorical one-word questions, hashtag walls, engagement bait and uniform sentence length are flagged for rewriting rather than modified blindly.

The five local checks are burstiness, specificity, slop density, fingerprint and voice. They are heuristics, not external detector APIs, and they do not promise that text is "undetectable".

## Codex state files

The skills use these user-local files when available:

```text
~/.codex/linkedin/voice.md
~/.codex/linkedin/log.md
~/.codex/linkedin/plan.md
```

`voice.md` stores style guidance. `log.md` stores the post/history notes used by `$li-audit`. `plan.md` stores the weekly plan used across the pack.

## Safety and LinkedIn automation

These skills do **not** publish, comment, connect, send DMs or scrape LinkedIn automatically. They produce copy-ready text for the user to post manually.

That approval boundary is intentional. It avoids browser automation and automated outreach patterns that can violate LinkedIn's terms or put an account at risk.

Nothing here should fabricate metrics, clients, outcomes or mutual connections. If a draft needs a fact the user has not supplied, it should be requested or clearly left unresolved.

## Files

```text
.codex-plugin/plugin.json        Codex plugin manifest
skills/li-post/hooks.json        21 hook formulas
skills/li-human/slop.json        humanizer lexicon and structural tells
skills/li-human/humanize.py      cleaning passes
skills/li-human/detect.py        five-check panel
skills/li-profile/rubric.json    100-point profile rubric
templates/voice.md               voice profile template
```

## Credit

Original skill pack by Jake Schincariol, [opusjake.ai](https://opusjake.ai).
Original repository: [Jakeschincariol/linkedin-agent-skill](https://github.com/Jakeschincariol/linkedin-agent-skill).

Codex port maintained in this fork by Ryo Aizawa.

## License

MIT. See [LICENSE](LICENSE).
