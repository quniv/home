<!-- src/pages/Blog.svelte — Lab notes + blog feed -->
<script>
  import { labNotes } from '../orgData.js';
  import { onMount } from 'svelte';

  const published = labNotes.filter(n => n.status === 'published');

  const pendingLines = [
    '> [ChillPickle] Booting blog engine...',
    '> [ChillPickle] Scanning lab notes...',
    '> [PENDING] Lab notes — coming soon',
    '> [PENDING] Blog posts — coming soon',
    '> Stand by.',
  ];

  let visibleLines = [];
  let showCursor = true;

  onMount(() => {
    if (published.length === 0) {
      pendingLines.forEach((line, i) => {
        setTimeout(() => {
          visibleLines = [...visibleLines, line];
        }, i * 600);
      });
    }

    const id = setInterval(() => { showCursor = !showCursor; }, 530);
    return () => clearInterval(id);
  });

  const typeLabel = { lab: 'LAB', blog: 'BLOG' };
</script>

<style>
  /* ── Page header ── */
  .page-header {
    background: linear-gradient(180deg, rgba(5, 3, 20, 0.98) 0%, rgba(5, 5, 25, 0.95) 100%);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(167, 139, 250, 0.15);
    padding: 2.5rem 2rem 2rem;
    position: relative;
  }

  .page-header::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(167, 139, 250, 0.4), transparent);
  }

  .page-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 1.4rem;
    font-weight: 700;
    color: #f0ecff;
    letter-spacing: 3px;
    margin: 0 0 0.3rem;
  }

  .page-subtitle {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    color: #a78bfa;
    letter-spacing: 2px;
    margin: 0;
  }

  /* ── Main ── */
  main {
    padding: 2.5rem 2rem;
    max-width: 900px;
    margin: 0 auto;
  }

  /* ── Terminal (pending state) ── */
  .terminal-wrap {
    background: rgba(5, 3, 20, 0.9);
    border: 1px solid rgba(167, 139, 250, 0.25);
    border-radius: 4px;
    overflow: hidden;
    box-shadow: 0 0 30px rgba(167, 139, 250, 0.08);
  }

  .terminal-bar {
    display: flex;
    align-items: center;
    gap: 0.45rem;
    padding: 0.65rem 1rem;
    background: rgba(167, 139, 250, 0.06);
    border-bottom: 1px solid rgba(167, 139, 250, 0.15);
  }

  .dot {
    width: 11px;
    height: 11px;
    border-radius: 50%;
  }

  .dot.red    { background: #f472b6; box-shadow: 0 0 6px rgba(244, 114, 182, 0.5); }
  .dot.yellow { background: #fbbf24; box-shadow: 0 0 6px rgba(251, 191, 36, 0.5); }
  .dot.green  { background: #a78bfa; box-shadow: 0 0 6px rgba(167, 139, 250, 0.5); }

  .terminal-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    color: #6b5a9e;
    letter-spacing: 2px;
    margin-left: 0.5rem;
  }

  .terminal-body {
    padding: 1.5rem 1.5rem 1.2rem;
    min-height: 160px;
  }

  .terminal-line {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.82rem;
    color: #a78bfa;
    line-height: 1.9;
    white-space: pre;
  }

  .terminal-line.pending {
    color: #9d8ec4;
  }

  /* ── Published posts ── */
  .posts-list {
    display: flex;
    flex-direction: column;
    gap: 1.2rem;
    margin-bottom: 2rem;
  }

  .post-card {
    background: rgba(5, 3, 20, 0.85);
    backdrop-filter: blur(16px);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: 4px;
    padding: 1.6rem 1.8rem;
    transition: all 0.3s ease;
    box-shadow: 0 0 16px rgba(167, 139, 250, 0.05);
  }

  .post-card:hover {
    border-color: rgba(167, 139, 250, 0.4);
    transform: translateY(-2px);
    box-shadow: 0 0 24px rgba(167, 139, 250, 0.12);
  }

  .post-meta {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    margin-bottom: 0.7rem;
    flex-wrap: wrap;
  }

  .post-date {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.68rem;
    color: #fbbf24;
    letter-spacing: 1px;
  }

  .post-type {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.62rem;
    letter-spacing: 1.5px;
    padding: 0.15rem 0.5rem;
    border-radius: 2px;
    color: #a78bfa;
    background: rgba(167, 139, 250, 0.08);
    border: 1px solid rgba(167, 139, 250, 0.2);
  }

  .post-title {
    font-size: 1rem;
    font-weight: 600;
    color: #f0ecff;
    margin: 0 0 0.5rem;
    letter-spacing: 0.3px;
    line-height: 1.4;
  }

  .post-excerpt {
    font-size: 0.86rem;
    color: #9d8ec4;
    line-height: 1.7;
    margin: 0 0 0.9rem;
  }

  .post-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.35rem;
  }

  .post-tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.62rem;
    color: #6b5a9e;
    background: rgba(167, 139, 250, 0.05);
    border: 1px solid rgba(167, 139, 250, 0.12);
    border-radius: 2px;
    padding: 0.12rem 0.45rem;
    letter-spacing: 0.5px;
  }

  /* ── Cursor ── */
  .cursor-line {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.82rem;
    color: #4a4070;
    padding-top: 0.8rem;
    letter-spacing: 1px;
  }

  .cursor {
    display: inline-block;
    width: 8px;
    height: 0.9em;
    background: #a78bfa;
    vertical-align: text-bottom;
    margin-left: 2px;
    opacity: 0;
    transition: opacity 0.1s;
  }

  .cursor.visible {
    opacity: 0.7;
  }

  /* ── Responsive ── */
  @media (max-width: 768px) {
    main { padding: 1.5rem 1rem; }
  }
</style>

<div class="page-header">
  <div class="page-title">BLOG & LAB NOTES</div>
  <div class="page-subtitle">// notes.log</div>
</div>

<main>
  {#if published.length === 0}
    <div class="terminal-wrap">
      <div class="terminal-bar">
        <div class="dot red"></div>
        <div class="dot yellow"></div>
        <div class="dot green"></div>
        <span class="terminal-title">BLOG & LAB NOTES</span>
      </div>
      <div class="terminal-body">
        {#each visibleLines as line, i (i)}
          <div class="terminal-line" class:pending={line.includes('[PENDING]')}>{line}</div>
        {/each}
        <div class="cursor-line">
          &nbsp;<span class="cursor" class:visible={showCursor}></span>
        </div>
      </div>
    </div>
  {:else}
    <div class="posts-list">
      {#each published as post (post.id)}
        <div class="post-card">
          <div class="post-meta">
            <span class="post-date">{post.date}</span>
            <span class="post-type">[{typeLabel[post.type] ?? post.type.toUpperCase()}]</span>
          </div>
          <h3 class="post-title">{post.title}</h3>
          <p class="post-excerpt">{post.excerpt}</p>
          <div class="post-tags">
            {#each post.tags as t (t)}
              <span class="post-tag">{t}</span>
            {/each}
          </div>
        </div>
      {/each}
    </div>

    <div class="cursor-line">
      > // loading more...<span class="cursor" class:visible={showCursor}></span>
    </div>
  {/if}
</main>
