<script>
  import { onMount } from 'svelte';

  const lines = [
    '> Initializing news feed...',
    '> Connecting to data stream...',
    '> [PENDING] Daily news — coming soon',
    '> [PENDING] Announcements — coming soon',
    '> Stand by.',
  ];

  let visibleLines = [];

  onMount(() => {
    lines.forEach((line, i) => {
      setTimeout(() => {
        visibleLines = [...visibleLines, line];
      }, i * 600);
    });
  });
</script>

<style>
  .news-page {
    padding: var(--space-xl);
    max-width: 860px;
    margin: 0 auto;
  }

  .news-terminal {
    background: var(--surface-raised);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    border: 1px solid var(--border);
    border-radius: var(--radius-md);
    box-shadow: 0 4px 28px rgba(0, 0, 0, 0.4);
    overflow: hidden;
  }

  .terminal-bar {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 0.65rem 1rem;
    background: var(--accent-faint);
    border-bottom: 1px solid var(--border-subtle);
  }

  .t-dot {
    width: 10px;
    height: 10px;
    border-radius: 50%;
  }

  /* Muted traffic-light dots — no neon glow */
  .t-dot.red    { background: #c05070; }
  .t-dot.yellow { background: #b08830; }
  .t-dot.green  { background: var(--accent); }

  .terminal-label {
    margin-left: 0.5rem;
    color: var(--text-muted);
    font-family: var(--font-mono);
    font-size: 0.78rem;
    letter-spacing: 0.8px;
  }

  .terminal-body {
    padding: 1.75rem 2rem;
    font-family: var(--font-mono);
    font-size: 0.88rem;
    min-height: 240px;
    line-height: 1;
  }

  .terminal-line {
    color: var(--accent);
    line-height: 2.1;
    animation: fadeIn 0.25s ease-out;
    white-space: pre;
  }

  .terminal-line.pending {
    color: var(--text-muted);
  }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(3px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .cursor-line {
    display: flex;
    align-items: center;
    margin-top: 0.4rem;
  }

  .blink-cursor {
    display: inline-block;
    width: 8px;
    height: 1em;
    background: var(--accent);
    animation: cursorBlink 0.9s step-end infinite;
    vertical-align: middle;
    border-radius: 1px;
  }

  @keyframes cursorBlink {
    0%, 100% { opacity: 1; }
    50%       { opacity: 0; }
  }

  .news-header {
    margin-bottom: var(--space-xl);
    padding-top: var(--space-xl);
  }

  .news-header h1 {
    color: var(--text-primary);
    font-size: 1.55rem;
    font-weight: 300;
    letter-spacing: 5px;
    text-transform: uppercase;
    margin: 0 0 0.35rem;
    font-family: var(--font-mono);
  }

  .news-header .subtitle {
    color: var(--text-dim);
    font-size: 0.78rem;
    letter-spacing: 2.5px;
    font-family: var(--font-mono);
  }
</style>

<div class="news-page">
  <div class="news-header">
    <h1>News</h1>
    <div class="subtitle">// feed.log</div>
  </div>

  <div class="news-terminal">
    <div class="terminal-bar">
      <div class="t-dot red"></div>
      <div class="t-dot yellow"></div>
      <div class="t-dot green"></div>
      <span class="terminal-label">~/qitpy/news.feed</span>
    </div>
    <div class="terminal-body">
      {#each visibleLines as line (line)}
        <div class="terminal-line" class:pending={line.includes('[PENDING]')}>{line}</div>
      {/each}
      <div class="cursor-line">
        <span class="blink-cursor"></span>
      </div>
    </div>
  </div>
</div>
