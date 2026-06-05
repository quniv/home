<!-- src/pages/Home.svelte — Landing page -->
<script>
  import { org, missions } from '../orgData.js';
  import TechStack from '../components/TechStack.svelte';
  import TerminalBoot from '../components/TerminalBoot.svelte';

  export let onNavigate = () => {};
</script>

<style>
  /* ── Hero ── */
  header.hero {
    background: linear-gradient(180deg, rgba(5, 3, 20, 0.98) 0%, rgba(5, 5, 25, 0.95) 100%);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(167, 139, 250, 0.2);
    padding: 5rem 2rem 4rem;
    text-align: center;
    position: relative;
    overflow: hidden;
  }

  header.hero::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 2px;
    background: linear-gradient(90deg, transparent, #a78bfa, #fbbf24, #f472b6, #a78bfa, transparent);
    background-size: 200% 100%;
    animation: shimmer 4s linear infinite;
  }

  @keyframes shimmer {
    0%   { background-position: 200% 0; }
    100% { background-position: -200% 0; }
  }

  .org-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    letter-spacing: 4px;
    color: #a78bfa;
    text-shadow: 0 0 8px rgba(167, 139, 250, 0.5);
    margin-bottom: 1.2rem;
  }

  .org-name {
    font-size: clamp(2.4rem, 6vw, 4rem);
    font-weight: 700;
    color: #f0ecff;
    letter-spacing: -0.5px;
    margin-bottom: 1rem;
    line-height: 1.1;
  }

  .org-name span {
    color: #a78bfa;
  }

  .tagline {
    font-size: 1.15rem;
    color: #9d8ec4;
    font-weight: 300;
    letter-spacing: 0.5px;
    max-width: 520px;
    margin: 0 auto 2.5rem;
    line-height: 1.7;
  }

  .cta-group {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-wrap: wrap;
  }

  .cta-btn {
    display: inline-block;
    padding: 0.65rem 1.8rem;
    background: transparent;
    border: none;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.8rem;
    font-weight: 500;
    letter-spacing: 2px;
    text-transform: uppercase;
    cursor: pointer;
    transition: transform 0.2s, box-shadow 0.2s, background 0.2s;
    border-radius: 0;
  }

  .cta-btn.primary {
    color: #a78bfa;
    box-shadow: 0 0 12px rgba(167, 139, 250, 0.2), inset 0 0 0 1px rgba(167, 139, 250, 0.4);
  }

  .cta-btn.primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 25px rgba(167, 139, 250, 0.4), inset 0 0 0 1px #a78bfa;
    background: rgba(167, 139, 250, 0.08);
  }

  .cta-btn.secondary {
    color: #fbbf24;
    box-shadow: 0 0 12px rgba(251, 191, 36, 0.15), inset 0 0 0 1px rgba(251, 191, 36, 0.3);
  }

  .cta-btn.secondary:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 25px rgba(251, 191, 36, 0.3), inset 0 0 0 1px #fbbf24;
    background: rgba(251, 191, 36, 0.06);
  }

  /* ── Main ── */
  main {
    padding: 3rem 2rem;
    max-width: 1100px;
    margin: 0 auto;
  }

  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 3px;
    color: #a78bfa;
    margin-bottom: 1.8rem;
    text-transform: uppercase;
  }

  /* ── Mission Cards ── */
  .missions-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.5rem;
    margin-bottom: 4rem;
  }

  .mission-card {
    background: rgba(5, 3, 20, 0.85);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: 4px;
    padding: 2rem 1.8rem;
    box-shadow: 0 0 20px rgba(167, 139, 250, 0.06), inset 0 0 20px rgba(167, 139, 250, 0.02);
    transition: all 0.4s ease;
  }

  .mission-card:hover {
    box-shadow: 0 0 30px rgba(167, 139, 250, 0.18), inset 0 0 20px rgba(167, 139, 250, 0.04);
    transform: translateY(-4px);
    border-color: rgba(167, 139, 250, 0.45);
  }

  .mission-icon {
    font-size: 2rem;
    margin-bottom: 1rem;
  }

  .mission-card h3 {
    font-size: 1rem;
    font-weight: 600;
    color: #f0ecff;
    margin: 0 0 0.75rem;
    letter-spacing: 0.5px;
  }

  .mission-card p {
    font-size: 0.9rem;
    color: #9d8ec4;
    line-height: 1.7;
    margin: 0;
  }

  /* ── Stack section ── */
  .section-stack {
    margin-bottom: 2rem;
  }

  /* ── Footer ── */
  footer {
    background: rgba(5, 3, 20, 0.95);
    backdrop-filter: blur(16px);
    border-top: 1px solid rgba(167, 139, 250, 0.15);
    color: #4a4070;
    text-align: center;
    padding: 1.8rem 2rem;
    position: relative;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    letter-spacing: 1px;
  }

  footer::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 2px;
    background: linear-gradient(90deg, transparent, #a78bfa, #fbbf24, #f472b6, #a78bfa, transparent);
    background-size: 200% 100%;
    animation: shimmer 4s linear infinite;
  }

  /* ── Responsive ── */
  @media (max-width: 900px) {
    .missions-grid {
      grid-template-columns: 1fr;
    }
  }

  @media (max-width: 768px) {
    header.hero {
      padding: 4rem 1.5rem 3rem;
    }

    main {
      padding: 2rem 1rem;
    }
  }
</style>

<TerminalBoot />

<header class="hero">
  <div class="org-label">// CHILLPICKLE.ORG</div>
  <h1 class="org-name">Chill<span>Pickle</span></h1>
  <p class="tagline">{org.tagline}</p>
  <div class="cta-group">
    <button class="cta-btn primary" on:click={() => onNavigate('work')}>[↗ View Work]</button>
    <button class="cta-btn secondary" on:click={() => onNavigate('services')}>[→ Get in Touch]</button>
  </div>
</header>

<main>
  <div class="section-label">// MISSION</div>
  <div class="missions-grid">
    {#each missions as m (m.id)}
      <div class="mission-card">
        <div class="mission-icon">{m.icon}</div>
        <h3>{m.title}</h3>
        <p>{m.body}</p>
      </div>
    {/each}
  </div>

  <div class="section-stack">
    <div class="section-label">// STACK</div>
    <TechStack />
  </div>
</main>

<footer>
  <p>© 2025 ChillPickle · Open for work · {org.domain}</p>
</footer>
