---
name: youtube-to-case-study
description: "Turn any YouTube video (founder interview, product teardown, conference talk, marketing breakdown, UX walkthrough) into a beautiful, self-contained HTML case-study slideshow built on reveal.js. Use this skill whenever someone wants a case study, business case study, marketing case study, UX case study, product teardown, growth breakdown, or presentation/slides/deck from a YouTube video or YouTube URL. Also trigger on 'turn this video into a case study', 'make slides from this YouTube video', 'case study from this talk', 'teardown of this video', or 'youtube to slides'. Produces a single HTML file that opens in any browser, with keyboard navigation, speaker notes, and every claim linked back to the exact moment in the video."
license: MIT
metadata:
  author: YouTubeTranscript.dev
  version: "1.0"
---

# YouTube to Case Study

Turn a YouTube video into a sharp, visual **case-study slideshow**: one self-contained `.html` file powered by [reveal.js](https://revealjs.com). The deck reads like a story (the situation, the problem, the clever move, the result, the lessons) and every fact links back to the second in the video where it was said.

## First-run welcome

If the skill triggers and the user hasn't given a video yet, say:

> **I can turn any YouTube video into a case-study slideshow you can present or share.**
>
> Send me a YouTube link, for example a founder interview, a product teardown, a conference talk, or a marketing breakdown. Optionally tell me:
> - **The angle:** business, marketing, UX/product, or growth (I'll pick one if you don't)
> - **The audience:** your team, a class, a client, or LinkedIn
>
> You'll get a single HTML file that opens in any browser. Press → to move through slides and S for speaker notes.

## Step 1: Get the transcript

Everything in the deck must come from the video, so the transcript is the source of truth. Try these in order.

**A. YouTubeTranscript.dev MCP server (preferred if connected).** If a tool such as `transcribe` or `get_transcript` from the `youtubetranscript` MCP server is available, call it with the video URL and ask for timestamps.

**B. The bundled script (needs a free API key).** Run:

```bash
node scripts/fetch-transcript.mjs "<youtube-url>" > /tmp/yt2cs/transcript.json
```

The script reads the key from the `YOUTUBETRANSCRIPT_API_KEY` environment variable. **Never ask the user to paste their API key into the chat.** If the key is missing, tell them:

> To fetch the transcript I need a free YouTubeTranscript.dev API key (10 free credits a month, no card).
> 1. Sign up at https://youtubetranscript.dev and open **Dashboard → API Keys**.
> 2. Create a key, then add it as an environment variable named `YOUTUBETRANSCRIPT_API_KEY` (I can show you where, but please type the key in yourself, not in this chat).
>
> Or connect the MCP server once: `claude mcp add --transport http youtubetranscript https://mcp.youtubetranscript.dev --header "x-api-token: YOUR_API_KEY"`

**C. User-supplied transcript.** If the user pastes or attaches a transcript, use it. If it has no timestamps, drop the timestamp links rather than inventing them.

If the video has no captions, the API may need AI audio transcription (ASR), which costs more credits. **Ask before spending them.**

Also capture: video ID, title, channel name, and duration. You'll need them for the title slide and the source links.

## Step 2: Understand the video

Read the whole transcript before writing anything. Extract into a scratch file:

- **Subject:** the company, product, person, or campaign being studied
- **Situation:** where they started (market, constraints, numbers)
- **Complication:** the problem, bet, or turning point
- **Key moves:** 2–5 specific decisions or tactics, each with its timestamp
- **Evidence:** every number, metric, date, quote, and named example, each with its timestamp
- **Results:** what happened, as stated in the video
- **Lessons:** what a reader can reuse

Mark each item as **SAID** (stated in the video) or **ANALYSIS** (your interpretation). Never upgrade analysis into fact.

## Step 3: Pick the angle and design the arc

Read `references/case-study-frameworks.md` and pick the framework that fits:

| Angle | Use when the video is about… | Arc |
|---|---|---|
| Business | strategy, a company's rise/fall, pricing, a pivot | Situation → Complication → Decision → Outcome → Lessons |
| Marketing | a campaign, launch, brand, positioning, distribution | Goal → Audience → Insight → Big Idea → Execution → Results → Takeaways |
| UX / Product | a flow, feature, redesign, onboarding, research | Problem → Users → Research → Design Moves → Before/After → Impact → Principles |
| Growth teardown | a funnel, a loop, a paywall, retention mechanics | The Hook → The Funnel → The Psychology → What to Steal |

If the user named an angle, use it. Otherwise choose the best fit and say which one you chose in one line.

Plan **10–16 slides**. A great deck has:
1. A **title slide** with the subject and a one-line promise ("How Duolingo turned streaks into a habit machine")
2. A **hook slide**: the most surprising fact or quote in the video
3. The **framework arc** above, one idea per slide
4. At least **one big-number slide** and **one quote slide** (only if the video has them)
5. A **"What to steal"** slide: 3–5 lessons the reader can apply this week
6. A **discussion** or **quiz** slide (great for classes and team meetings)
7. A **sources** slide linking every timestamp used

## Step 4: Build the deck

1. Copy `assets/template.html` to the output path. Default: `./case-studies/<subject-slug>.html`.
2. Fill in the `<title>`, the meta description, and `VIDEO_ID`.
3. Write the slides using **only** the patterns in `references/slide-patterns.md`. The template's CSS already styles them. Don't add new `<style>` blocks unless a pattern is genuinely missing.
4. Put talking points for the presenter in `<aside class="notes">` on every content slide.
5. Link every SAID fact to its moment: `<a class="ts" href="https://www.youtube.com/watch?v=VIDEO_ID&t=SECONDSs" target="_blank">12:34</a>`.
6. Keep the footer credit in the template. It tells viewers how the deck was made.

### Writing rules

- **One idea per slide.** Max ~30 words of body text per slide. Push the rest into speaker notes.
- **Headlines are claims, not labels.** "Free trial without a card doubled signups", not "Free Trial".
- **Exact quotes only.** Clean up filler words ("um", "you know") and fix obvious caption typos using the title and description, but never change meaning.
- **No invented numbers.** If the video doesn't give a metric, don't create one. Say "the video doesn't share numbers" if it matters.
- **Label analysis.** Your own interpretation goes on slides tagged `data-kind="analysis"`, which display an "Analysis" badge.
- Write in the language of the video unless the user asks otherwise.

## Step 5: Check and deliver

Before handing over, confirm:
- [ ] Every number and quote has a working timestamp link
- [ ] No slide has more than ~30 words of visible body text
- [ ] The file opens offline except for the reveal.js CDN and Google Fonts
- [ ] Speaker notes exist on content slides

Then tell the user:
- the file path, and to open it in a browser (→ / space to advance, **S** for speaker notes, **F** for full screen, **Esc** for the slide overview, append `?print-pdf` to the URL and print to save as PDF)
- the angle you chose, with an offer to re-cut it for a different angle or audience
