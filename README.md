# YouTube to Case Study

**Turn any YouTube video into a beautiful case-study slideshow in one prompt.**

A free, open-source skill for Claude Code (and other AI coding agents). Paste a YouTube link, such as a founder interview, product teardown, conference talk, or marketing breakdown, and get back a polished **business case study**, **marketing case study**, **UX case study**, or **growth teardown** as a single HTML slideshow you can present, share, or save as PDF.

Every fact in the deck links to the exact second in the video where it was said.

---

## What you get

A single `.html` file built on [reveal.js](https://revealjs.com). It opens in any browser, with no install and no account.

- **A story, not a summary.** Situation → problem → the clever move → result → lessons
- **Four case-study styles:** Business, Marketing, UX / Product, and Growth teardown
- **Timestamp receipts.** Every number and quote links to its moment on YouTube
- **Slides built for presenting:** big numbers, pull quotes, before/after comparisons, step-by-step journeys, "what to steal" cards
- **Speaker notes** on every slide (press **S**)
- **Discussion and quiz slides** for classrooms, workshops, and team meetings
- **Light and dark mode**, keyboard navigation, overview mode (**Esc**), and PDF export
- **Honest by design.** Your agent's own interpretation is labeled "Analysis" and never passed off as fact

## Who it's for

- **Product managers and designers** turning a great talk into a team share-out
- **Marketers** building swipe files of campaigns and launches
- **Students and teachers** who need a business or marketing case study for class
- **Founders and consultants** making client-ready teardowns
- **UX designers** collecting UX case studies and design-pattern references

## Install with your coding agent

You don't need to use the command line. Send this message to Claude Code (or your coding agent of choice):

> Install the youtube-to-case-study skill from https://github.com/tstfully/youtube-to-case-study into my Claude skills folder (`~/.claude/skills/youtube-to-case-study`). Then help me connect a free YouTubeTranscript.dev API key, without me pasting the key into this chat.

### Or install manually

```bash
git clone https://github.com/tstfully/youtube-to-case-study ~/.claude/skills/youtube-to-case-study
```

## Connect transcripts (free)

The skill reads the video's transcript, so it needs a transcript source. Pick one.

**Option 1: MCP server (recommended for Claude Code, Claude Desktop, Cursor)**

```bash
claude mcp add --transport http youtubetranscript https://mcp.youtubetranscript.dev --header "x-api-token: YOUR_API_KEY"
```

**Option 2: Environment variable.** Set `YOUTUBETRANSCRIPT_API_KEY` to your key. The skill's built-in script (`scripts/fetch-transcript.mjs`, no dependencies) uses it.

Get your key free at [youtubetranscript.dev](https://youtubetranscript.dev) under **Dashboard → API Keys**. The free plan includes 10 credits a month and needs no card. Most videos cost 1 credit.

> 🔒 Never paste an API key into an AI chat, a screenshot, or a public file. Type it directly into your terminal or settings.

**Option 3: Paste a transcript.** Already have the transcript? Paste it in and the skill works without any key. Without timestamps, the deck won't have links back to the video.

## Use it

Just ask:

- *"Turn this video into a case study: https://youtube.com/watch?v=…"*
- *"Make a marketing case study from this talk for my team"*
- *"UX case study from this video, as slides"*
- *"Growth teardown of this video, growth.design style"*
- *"Business case study for my MBA class, with discussion questions"*

The skill picks the best angle if you don't specify one, and tells you which it chose. Ask it to re-cut the same video for a different angle or audience any time.

### Presenting

| Key | Action |
|---|---|
| → / Space | Next slide |
| S | Speaker notes window |
| F | Full screen |
| Esc | Slide overview |

**Save as PDF:** add `?print-pdf` to the end of the file's URL in Chrome, then print and choose **Save as PDF**.

## How it works

```
YouTube URL
   │
   ▼
Transcript (YouTubeTranscript.dev: captions in 100+ languages, AI transcription when there are none)
   │
   ▼
Your AI agent reads the full transcript → extracts facts, quotes, numbers, timestamps
   │
   ▼
Picks a case-study framework → plans 10–16 slides
   │
   ▼
Fills a pre-built reveal.js template → one self-contained HTML file
```

## Repo structure

```
youtube-to-case-study/
├── SKILL.md                          # Instructions the AI agent follows
├── assets/template.html              # reveal.js template with the full design system
├── references/
│   ├── case-study-frameworks.md      # Business, Marketing, UX, Growth arcs
│   └── slide-patterns.md             # Every slide type as copy-ready HTML
└── scripts/fetch-transcript.mjs      # Zero-dependency transcript fetcher
```

## Companion skills

- [youtube-to-course](https://github.com/tstfully/youtube-to-course): turn a video into an interactive course with quizzes and flashcards
- [youtube-to-ai-chat](https://github.com/tstfully/youtube-to-ai-chat): chat with any YouTube video, with answers cited to the second

## More from YouTubeTranscript.dev

- [YouTube Transcript API](https://github.com/Youtube-Transcript-Dev/Youtube-Transcript-API): REST API, examples, and an API skill
- [MCP server](https://github.com/Youtube-Transcript-Dev/youtube-transcript-mcp): YouTube transcripts inside any AI assistant
- SDKs for [Node.js](https://github.com/Youtube-Transcript-Dev/youtube-transcript-sdk), [Python](https://github.com/Youtube-Transcript-Dev/youtube-transcript-python-sdk), and [Dart](https://github.com/Youtube-Transcript-Dev/dart-sdk)
- [Free online tools](https://www.youtubetranscript.dev/tools): transcripts, summaries, chapters, and more, no login required

## License

MIT. Use it, fork it, and build on it. Slides are rendered with [reveal.js](https://github.com/hakimel/reveal.js) (MIT), loaded from the cdnjs CDN.
