# Slide Patterns

> **When to read this:** Step 4, while writing slides. Use only these patterns. `assets/template.html` already contains the CSS for every one of them.

Every slide is a `<section>` inside `<div class="slides">`. Add `<aside class="notes">…</aside>` with presenter talking points on every content slide.

Timestamp links always look like this (replace `VIDEO_ID` and the seconds):

```html
<a class="ts" href="https://www.youtube.com/watch?v=VIDEO_ID&t=754s" target="_blank">12:34</a>
```

---

## Title

```html
<section class="slide-title">
  <p class="eyebrow">Marketing case study</p>
  <h1>How Duolingo turned a streak into a habit machine</h1>
  <p class="source">From <strong>“Video title”</strong> · Channel name · 42 min</p>
</section>
```

## Hook (surprising fact or quote)

```html
<section class="slide-hook">
  <p class="eyebrow">The hook</p>
  <h2>They deleted the free trial, and signups went up.</h2>
  <a class="ts" href="…&t=312s" target="_blank">5:12</a>
  <aside class="notes">Why this is surprising, and what to set up next.</aside>
</section>
```

## Section divider

```html
<section class="slide-divider" data-step="02">
  <h2>The Decision</h2>
</section>
```

## Claim + supporting points

```html
<section>
  <p class="eyebrow">Situation</p>
  <h2>A crowded market with no clear winner</h2>
  <ul class="points">
    <li>Five funded competitors in 2019 <a class="ts" href="…&t=95s" target="_blank">1:35</a></li>
    <li>Customers churned within 3 months <a class="ts" href="…&t=140s" target="_blank">2:20</a></li>
  </ul>
  <aside class="notes">…</aside>
</section>
```

## Big number

Only use numbers that are SAID in the video.

```html
<section class="slide-big">
  <p class="big">3×</p>
  <p class="caption">more daily learners after streak freezes launched</p>
  <a class="ts" href="…&t=1210s" target="_blank">20:10</a>
</section>
```

## Stat strip (2–4 numbers)

```html
<section>
  <h2>The starting point</h2>
  <div class="stats">
    <div class="stat"><span class="num">$2M</span><span class="label">ARR</span></div>
    <div class="stat"><span class="num">12</span><span class="label">employees</span></div>
    <div class="stat"><span class="num">40%</span><span class="label">monthly churn</span></div>
  </div>
</section>
```

## Quote

```html
<section class="slide-quote">
  <blockquote>We stopped asking what users want and started watching what they do.</blockquote>
  <p class="who">Jane Doe, Head of Product <a class="ts" href="…&t=845s" target="_blank">14:05</a></p>
</section>
```

## Before / after

```html
<section>
  <h2>Onboarding went from a form to a first win</h2>
  <div class="compare">
    <div class="col before"><span class="tag">Before</span><p>7-field signup before seeing the product</p></div>
    <div class="col after"><span class="tag">After</span><p>Try a lesson first, sign up after</p></div>
  </div>
</section>
```

## Numbered steps (journey, execution, funnel)

```html
<section>
  <h2>The launch, step by step</h2>
  <ol class="steps">
    <li><strong>Waitlist</strong><span>Invite-only for 6 weeks</span></li>
    <li><strong>Creators</strong><span>200 YouTubers got early access</span></li>
    <li><strong>Public</strong><span>Opened on Product Hunt day</span></li>
  </ol>
</section>
```

## Cards (lessons, principles, "what to steal")

```html
<section>
  <p class="eyebrow">What to steal</p>
  <h2>Three moves you can copy this week</h2>
  <div class="cards">
    <div class="card"><span class="icon">⚡</span><h3>Value before signup</h3><p>Let people try one thing before asking for an email.</p></div>
    <div class="card"><span class="icon">🔥</span><h3>Make progress visible</h3><p>Show a streak or counter from day one.</p></div>
    <div class="card"><span class="icon">🧊</span><h3>Forgive one miss</h3><p>A “freeze” keeps people from quitting after a slip.</p></div>
  </div>
</section>
```

## Analysis slide

Any slide that is mostly your interpretation gets `data-kind="analysis"`. The template adds an "Analysis" badge automatically.

```html
<section data-kind="analysis">
  <h2>Why it worked: loss aversion</h2>
  <p class="lead">Losing a 100-day streak feels worse than gaining one more day feels good.</p>
</section>
```

## Discussion / quiz

Click-to-reveal works with reveal.js fragments (press → to reveal).

```html
<section class="slide-quiz">
  <p class="eyebrow">Your turn</p>
  <h2>Their churn spiked in month 3. What would you test first?</h2>
  <ul class="options">
    <li>A. A cheaper plan</li>
    <li>B. A month-2 check-in email</li>
    <li>C. A loyalty discount</li>
  </ul>
  <p class="fragment answer">What they did: <strong>B</strong>, a check-in at day 45 <a class="ts" href="…&t=1500s" target="_blank">25:00</a></p>
</section>
```

## Sources

```html
<section class="slide-sources">
  <h2>Sources</h2>
  <p>All facts from <a href="https://www.youtube.com/watch?v=VIDEO_ID" target="_blank">“Video title”</a> by Channel name.</p>
  <ul class="source-list">
    <li><a class="ts" href="…&t=95s" target="_blank">1:35</a> Market size and competitors</li>
    <li><a class="ts" href="…&t=312s" target="_blank">5:12</a> Removing the free trial</li>
  </ul>
</section>
```
