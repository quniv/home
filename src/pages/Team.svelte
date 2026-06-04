<!-- src/pages/Team.svelte — Team member cards -->
<script>
  import { team } from '../orgData.js';
  import GameOfLife from '../components/GameOfLife.svelte';

  const SLOTS = 4;
  const emptySlotIndices = Array.from({ length: SLOTS - team.length }, (_, i) => i);
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

  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 3px;
    color: #a78bfa;
    margin-bottom: 1.6rem;
    text-transform: uppercase;
  }

  /* ── Mission strip ── */
  .mission-strip {
    font-style: italic;
    font-size: 0.95rem;
    color: #9d8ec4;
    letter-spacing: 0.5px;
    margin-bottom: 2.5rem;
    line-height: 1.7;
  }

  /* ── Team grid ── */
  .team-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1.2rem;
    margin-bottom: 3.5rem;
  }

  /* ── Member card ── */
  .member-card {
    background: rgba(5, 3, 20, 0.85);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    border: 1px solid rgba(167, 139, 250, 0.25);
    border-radius: 4px;
    padding: 2rem 1.5rem;
    text-align: center;
    box-shadow: 0 0 20px rgba(167, 139, 250, 0.08), inset 0 0 20px rgba(167, 139, 250, 0.02);
    transition: all 0.4s ease;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.6rem;
  }

  .member-card:hover {
    box-shadow: 0 0 30px rgba(167, 139, 250, 0.2), inset 0 0 20px rgba(167, 139, 250, 0.04);
    transform: translateY(-4px);
    border-color: rgba(167, 139, 250, 0.5);
  }

  .member-avatar {
    width: 90px;
    height: 90px;
    border-radius: 50%;
    border: 2px solid rgba(167, 139, 250, 0.4);
    margin-bottom: 0.4rem;
    transition: all 0.4s ease;
    box-shadow: 0 0 16px rgba(167, 139, 250, 0.15);
    object-fit: cover;
  }

  .member-card:hover .member-avatar {
    border-color: #a78bfa;
    box-shadow: 0 0 24px rgba(167, 139, 250, 0.35);
  }

  .member-name {
    font-size: 0.95rem;
    font-weight: 600;
    color: #f0ecff;
    margin: 0;
    letter-spacing: 0.5px;
  }

  .member-role {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.68rem;
    color: #a78bfa;
    letter-spacing: 1.5px;
    text-shadow: 0 0 6px rgba(167, 139, 250, 0.4);
  }

  .member-bio {
    font-size: 0.8rem;
    color: #7d6ea4;
    line-height: 1.6;
    margin: 0.3rem 0 0;
    text-align: left;
  }

  .skills-row {
    display: flex;
    flex-wrap: wrap;
    gap: 0.35rem;
    justify-content: center;
    margin-top: 0.2rem;
  }

  .skill-chip {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.6rem;
    color: #6b5a9e;
    background: rgba(167, 139, 250, 0.06);
    border: 1px solid rgba(167, 139, 250, 0.15);
    border-radius: 2px;
    padding: 0.15rem 0.45rem;
    letter-spacing: 0.5px;
  }

  .member-links {
    display: flex;
    gap: 0.6rem;
    margin-top: 0.4rem;
  }

  .member-link {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.68rem;
    color: #9d8ec4;
    text-decoration: none;
    letter-spacing: 1px;
    padding: 0.25rem 0.6rem;
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: 2px;
    transition: all 0.2s;
  }

  .member-link:hover {
    color: #a78bfa;
    border-color: rgba(167, 139, 250, 0.5);
    background: rgba(167, 139, 250, 0.06);
  }

  /* ── Empty slot card ── */
  .slot-empty {
    background: rgba(5, 3, 20, 0.4);
    border: 1px dashed rgba(167, 139, 250, 0.15);
    border-radius: 4px;
    padding: 2rem 1.5rem;
    text-align: center;
    opacity: 0.5;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    min-height: 160px;
  }

  .slot-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    color: #4a4070;
    letter-spacing: 2px;
  }

  /* ── Responsive ── */
  @media (max-width: 1000px) {
    .team-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 600px) {
    .team-grid {
      grid-template-columns: 1fr;
    }

    main { padding: 1.5rem 1rem; }
  }
</style>

<div class="page-header">
  <div class="page-title">TEAM</div>
  <div class="page-subtitle">// who we are</div>
</div>

<main>
  <div class="section-label">// PEOPLE</div>
  <p class="mission-strip">A small group of engineers who build things that actually work.</p>

  <div class="team-grid">
    {#each team as m (m.id)}
      <div class="member-card">
        <img class="member-avatar" src={m.avatar} alt={m.name} />
        <h3 class="member-name">{m.name}</h3>
        <div class="member-role">{m.role}</div>
        <p class="member-bio">{m.bio}</p>
        <div class="skills-row">
          {#each m.skills as s (s)}
            <span class="skill-chip">{s}</span>
          {/each}
        </div>
        <div class="member-links">
          {#if m.links.github}
            <a class="member-link" href={m.links.github} target="_blank" rel="noopener noreferrer">GitHub</a>
          {/if}
          {#if m.links.linkedin}
            <a class="member-link" href={m.links.linkedin} target="_blank" rel="noopener noreferrer">LinkedIn</a>
          {/if}
        </div>
      </div>
    {/each}

    {#each emptySlotIndices as idx (idx)}
      <div class="slot-empty">
        <div class="slot-label">+ TBD</div>
      </div>
    {/each}
  </div>

  <div class="section-label">// HOW WE WORK</div>
  <GameOfLife />
</main>
