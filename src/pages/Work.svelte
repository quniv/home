<!-- src/pages/Work.svelte — Projects showcase -->
<script>
  import { projects } from '../orgData.js';
  import { onMount } from 'svelte';

  let showCursor = true;
  onMount(() => {
    const id = setInterval(() => { showCursor = !showCursor; }, 530);
    return () => clearInterval(id);
  });
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
    max-width: 1100px;
    margin: 0 auto;
  }

  /* ── Project cards ── */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 1.5rem;
    margin-bottom: 3rem;
  }

  .project-card {
    background: rgba(5, 3, 20, 0.85);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: 4px;
    padding: 1.8rem;
    box-shadow: 0 0 20px rgba(167, 139, 250, 0.06), inset 0 0 20px rgba(167, 139, 250, 0.02);
    transition: all 0.35s ease;
    display: flex;
    flex-direction: column;
    gap: 0.9rem;
  }

  .project-card:hover {
    box-shadow: 0 0 30px rgba(167, 139, 250, 0.16), inset 0 0 20px rgba(167, 139, 250, 0.03);
    transform: translateY(-3px);
    border-color: rgba(167, 139, 250, 0.4);
  }

  .card-header {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    flex-wrap: wrap;
  }

  .project-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 1rem;
    font-weight: 600;
    color: #f0ecff;
    margin: 0;
    letter-spacing: 0.5px;
    flex: 1;
  }

  .status-badge {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 1.5px;
    padding: 0.2rem 0.55rem;
    border-radius: 2px;
    text-transform: uppercase;
    flex-shrink: 0;
  }

  .status-badge.live {
    color: #00ff78;
    background: rgba(0, 255, 120, 0.08);
    border: 1px solid rgba(0, 255, 120, 0.3);
    box-shadow: 0 0 8px rgba(0, 255, 120, 0.15);
  }

  .status-badge.wip {
    color: #fbbf24;
    background: rgba(251, 191, 36, 0.08);
    border: 1px solid rgba(251, 191, 36, 0.3);
  }

  .tag-chip {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 1px;
    padding: 0.2rem 0.55rem;
    border-radius: 2px;
    text-transform: uppercase;
  }

  .tag-chip.green {
    color: #00ff78;
    background: rgba(0, 255, 120, 0.06);
    border: 1px solid rgba(0, 255, 120, 0.2);
  }

  .tag-chip.purple {
    color: #a78bfa;
    background: rgba(167, 139, 250, 0.06);
    border: 1px solid rgba(167, 139, 250, 0.2);
  }

  .project-desc {
    font-size: 0.88rem;
    color: #9d8ec4;
    line-height: 1.7;
    margin: 0;
    flex: 1;
  }

  .stack-row {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
  }

  .stack-chip {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: #6b5a9e;
    background: rgba(167, 139, 250, 0.05);
    border: 1px solid rgba(167, 139, 250, 0.12);
    border-radius: 2px;
    padding: 0.15rem 0.5rem;
    letter-spacing: 0.5px;
  }

  .card-links {
    display: flex;
    gap: 0.75rem;
    flex-wrap: wrap;
  }

  .card-link {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    letter-spacing: 1.5px;
    padding: 0.35rem 0.9rem;
    background: transparent;
    border: none;
    text-decoration: none;
    cursor: pointer;
    transition: all 0.2s;
    border-radius: 0;
    color: #a78bfa;
    box-shadow: inset 0 0 0 1px rgba(167, 139, 250, 0.3);
  }

  .card-link:hover {
    box-shadow: inset 0 0 0 1px #a78bfa, 0 0 12px rgba(167, 139, 250, 0.2);
    background: rgba(167, 139, 250, 0.07);
  }

  /* ── Terminal footer ── */
  .terminal-footer {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.8rem;
    color: #4a4070;
    letter-spacing: 1px;
    padding: 1rem 0;
    border-top: 1px solid rgba(167, 139, 250, 0.1);
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
    .projects-grid { grid-template-columns: 1fr; }
  }
</style>

<div class="page-header">
  <div class="page-title">WORK / PROJECTS</div>
  <div class="page-subtitle">// projects.log</div>
</div>

<main>
  <div class="projects-grid">
    {#each projects as p (p.id)}
      <div class="project-card">
        <div class="card-header">
          <h3 class="project-title">{p.title}</h3>
          <span class="status-badge {p.status}">{p.status === 'live' ? '● live' : '○ wip'}</span>
          <span class="tag-chip {p.tagColor}">{p.tag}</span>
        </div>

        <p class="project-desc">{p.description}</p>

        {#if p.stack.length > 0}
          <div class="stack-row">
            {#each p.stack as s (s)}
              <span class="stack-chip">{s}</span>
            {/each}
          </div>
        {/if}

        {#if p.url || p.repo}
          <div class="card-links">
            {#if p.url}
              <a class="card-link" href={p.url} target="_blank" rel="noopener noreferrer">↗ Live</a>
            {/if}
            {#if p.repo}
              <a class="card-link" href={p.repo} target="_blank" rel="noopener noreferrer">⌥ Repo</a>
            {/if}
          </div>
        {/if}
      </div>
    {/each}
  </div>

  <div class="terminal-footer">
    > // more projects loading...<span class="cursor" class:visible={showCursor}></span>
  </div>
</main>
