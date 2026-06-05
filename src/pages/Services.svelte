<!-- src/pages/Services.svelte — Services + Pricing -->
<script>
  import { org, services, pricing } from '../orgData.js';
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

  /* ── Service cards ── */
  .services-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1.2rem;
    margin-bottom: 3.5rem;
  }

  .service-card {
    background: rgba(5, 3, 20, 0.85);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: 4px;
    padding: 1.8rem;
    box-shadow: 0 0 20px rgba(167, 139, 250, 0.06), inset 0 0 20px rgba(167, 139, 250, 0.02);
    transition: all 0.35s ease;
  }

  .service-card:hover {
    transform: translateY(-3px);
    border-color: rgba(167, 139, 250, 0.4);
    box-shadow: 0 0 30px rgba(167, 139, 250, 0.14), inset 0 0 20px rgba(167, 139, 250, 0.03);
  }

  @keyframes neonPulse {
    0%, 100% { box-shadow: 0 0 20px rgba(167, 139, 250, 0.15), inset 0 0 20px rgba(167, 139, 250, 0.03); }
    50%       { box-shadow: 0 0 35px rgba(167, 139, 250, 0.35), inset 0 0 25px rgba(167, 139, 250, 0.06); }
  }

  .service-card.highlight {
    border-color: rgba(167, 139, 250, 0.5);
    animation: neonPulse 3s ease-in-out infinite;
  }

  .service-card.highlight:hover {
    animation: none;
    box-shadow: 0 0 40px rgba(167, 139, 250, 0.4), inset 0 0 25px rgba(167, 139, 250, 0.06);
  }

  .service-icon {
    font-size: 1.6rem;
    margin-bottom: 0.8rem;
  }

  .service-title {
    font-size: 1rem;
    font-weight: 600;
    color: #f0ecff;
    margin: 0 0 0.6rem;
    letter-spacing: 0.5px;
  }

  .service-desc {
    font-size: 0.87rem;
    color: #9d8ec4;
    line-height: 1.7;
    margin: 0 0 1rem;
  }

  .tags-row {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
  }

  .tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: #6b5a9e;
    background: rgba(167, 139, 250, 0.06);
    border: 1px solid rgba(167, 139, 250, 0.15);
    border-radius: 2px;
    padding: 0.15rem 0.5rem;
    letter-spacing: 0.5px;
  }

  /* ── Pricing cards ── */
  .pricing-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.2rem;
    margin-bottom: 3rem;
  }

  .pricing-card {
    background: rgba(5, 3, 20, 0.85);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: 4px;
    padding: 2rem 1.6rem;
    display: flex;
    flex-direction: column;
    gap: 0.8rem;
    transition: all 0.35s ease;
    position: relative;
    overflow: hidden;
  }

  .pricing-card:hover {
    transform: translateY(-3px);
    border-color: rgba(167, 139, 250, 0.4);
    box-shadow: 0 0 30px rgba(167, 139, 250, 0.12);
  }

  @keyframes shimmer {
    0%   { background-position: 200% 0; }
    100% { background-position: -200% 0; }
  }

  .pricing-card.highlight::before {
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

  .pricing-card.highlight {
    border-color: rgba(167, 139, 250, 0.35);
    box-shadow: 0 0 20px rgba(167, 139, 250, 0.1);
  }

  .pricing-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 3px;
    color: #a78bfa;
    text-transform: uppercase;
  }

  .pricing-price {
    font-size: 1.5rem;
    font-weight: 700;
    color: #f0ecff;
    letter-spacing: -0.5px;
    line-height: 1;
  }

  .pricing-desc {
    font-size: 0.85rem;
    color: #9d8ec4;
    line-height: 1.6;
    margin: 0;
  }

  .pricing-bullets {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    gap: 0.4rem;
    flex: 1;
  }

  .pricing-bullets li {
    font-size: 0.83rem;
    color: #7d6ea4;
    padding-left: 1rem;
    position: relative;
    line-height: 1.5;
  }

  .pricing-bullets li::before {
    content: '›';
    position: absolute;
    left: 0;
    color: #a78bfa;
  }

  .contact-btn {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    letter-spacing: 1.5px;
    padding: 0.5rem 1rem;
    background: transparent;
    border: none;
    cursor: pointer;
    transition: all 0.2s;
    border-radius: 0;
    color: #a78bfa;
    box-shadow: inset 0 0 0 1px rgba(167, 139, 250, 0.3);
    text-decoration: none;
    display: inline-block;
    text-align: center;
    margin-top: auto;
  }

  .contact-btn:hover {
    box-shadow: inset 0 0 0 1px #a78bfa, 0 0 12px rgba(167, 139, 250, 0.2);
    background: rgba(167, 139, 250, 0.07);
  }

  /* ── Contact strip ── */
  .contact-strip {
    background: rgba(5, 3, 20, 0.85);
    backdrop-filter: blur(16px);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: 4px;
    padding: 2.5rem 2rem;
    text-align: center;
    box-shadow: 0 0 20px rgba(167, 139, 250, 0.06);
    margin-bottom: 2rem;
  }

  .contact-strip h3 {
    font-size: 1.1rem;
    font-weight: 600;
    color: #f0ecff;
    margin: 0 0 0.7rem;
    letter-spacing: 0.5px;
  }

  .contact-strip p {
    font-size: 0.88rem;
    color: #9d8ec4;
    margin: 0 0 1.2rem;
    line-height: 1.6;
  }

  .email-link {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.85rem;
    color: #a78bfa;
    text-decoration: none;
    letter-spacing: 1px;
    transition: all 0.2s;
  }

  .email-link:hover {
    color: #f0ecff;
    text-shadow: 0 0 8px rgba(167, 139, 250, 0.5);
  }

  .philosophy-note {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    color: #4a4070;
    letter-spacing: 2px;
    margin: 0.8rem 0 0;
  }

  /* ── Responsive ── */
  @media (max-width: 900px) {
    .services-grid  { grid-template-columns: 1fr; }
    .pricing-grid   { grid-template-columns: 1fr; }
  }

  @media (max-width: 768px) {
    main { padding: 1.5rem 1rem; }
  }
</style>

<div class="page-header">
  <div class="page-title">SERVICES / PRICING</div>
  <div class="page-subtitle">// what we do</div>
</div>

<main>
  <div class="section-label">// WHAT WE DO</div>
  <div class="services-grid">
    {#each services as s (s.id)}
      <div class="service-card" class:highlight={s.highlight}>
        <div class="service-icon">{s.icon}</div>
        <h3 class="service-title">{s.title}</h3>
        <p class="service-desc">{s.description}</p>
        <div class="tags-row">
          {#each s.tags as t (t)}
            <span class="tag">{t}</span>
          {/each}
        </div>
      </div>
    {/each}
  </div>

  <div class="section-label">// PRICING</div>
  <div class="pricing-grid">
    {#each pricing as p (p.id)}
      <div class="pricing-card" class:highlight={p.highlight}>
        <div class="pricing-label">{p.label}</div>
        <div class="pricing-price">{p.price}</div>
        <p class="pricing-desc">{p.description}</p>
        <ul class="pricing-bullets">
          {#each p.bullets as b, bi (bi)}
            <li>{b}</li>
          {/each}
        </ul>
        <a class="contact-btn" href="mailto:{org.email}">[→ Contact]</a>
      </div>
    {/each}
  </div>

  <div class="contact-strip">
    <h3>Ready to build something?</h3>
    <p>Tell us what you're trying to solve. We'll figure out if we're the right fit.</p>
    <a class="email-link" href="mailto:{org.email}">{org.email}</a>
    <p class="philosophy-note">reputation-based · affordable · ships</p>
  </div>
</main>
