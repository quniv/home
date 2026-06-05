<style>
  /* ── Growth Cycle Section ── */
  .recipe-section {
    background: var(--surface-raised);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    border: 1px solid var(--border);
    padding: var(--space-2xl) var(--space-xl);
    margin: var(--space-2xl) 0;
    text-align: center;
    border-radius: var(--radius-md);
    box-shadow: 0 4px 28px rgba(0, 0, 0, 0.35);
    position: relative;
    overflow: hidden;
  }

  .level-system {
    position: relative;
  }

  .level-indicator {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    margin-bottom: 1.75rem;
  }

  .level-bar {
    width: 200px;
    height: 5px;
    background: var(--accent-faint);
    border: 1px solid var(--border);
    border-radius: 3px;
    overflow: hidden;
  }

  .level-progress {
    height: 100%;
    width: 100%;
    background: linear-gradient(90deg, var(--accent), var(--gold), var(--accent));
    background-size: 200% 100%;
    animation: progressShift 3s linear infinite;
    border-radius: 3px;
  }

  @keyframes progressShift {
    0% { background-position: 0% 50%; }
    100% { background-position: 200% 50%; }
  }

  .level-text {
    color: var(--accent);
    font-size: 0.95rem;
    font-weight: 600;
    letter-spacing: 2.5px;
    font-family: var(--font-mono);
  }

  .cycle-container {
    display: flex;
    flex-direction: column;
    gap: 1.25rem;
    margin-bottom: 1.75rem;
  }

  .cycle-row {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 0.85rem;
    flex-wrap: wrap;
  }

  .cycle-step {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.35rem;
    padding: 1.1rem 1.1rem;
    background: rgba(8, 6, 24, 0.9);
    border: 1px solid var(--border);
    min-width: 124px;
    transition: transform 0.25s ease, border-color 0.25s ease, box-shadow 0.25s ease;
    position: relative;
    border-radius: var(--radius-sm);
  }

  .cycle-step:hover {
    transform: translateY(-4px);
    box-shadow: 0 6px 22px rgba(0, 0, 0, 0.45);
    border-color: var(--border-active);
  }

  .cycle-step .step-number {
    position: absolute;
    top: -10px;
    left: -10px;
    width: 22px;
    height: 22px;
    background: var(--accent);
    color: #0a0820;
    font-size: 0.72rem;
    font-weight: 700;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 3px;
    font-family: var(--font-mono);
  }

  .cycle-step .step-icon {
    font-size: 1.7rem;
  }

  .cycle-step .step-text {
    color: var(--text-primary);
    font-weight: 600;
    font-size: 0.83rem;
    letter-spacing: 0.5px;
  }

  .cycle-step .step-desc {
    color: var(--text-muted);
    font-size: 0.7rem;
    text-align: center;
    line-height: 1.4;
  }

  .cycle-step.damage {
    border-color: rgba(201, 93, 154, 0.35);
    background: rgba(18, 4, 12, 0.9);
  }

  .cycle-step.damage .step-number {
    background: var(--pink);
  }

  /* Muted green — no more #00ff78 neon */
  .cycle-step.growth {
    border-color: rgba(76, 175, 133, 0.35);
    background: rgba(4, 16, 10, 0.9);
  }

  .cycle-step.growth .step-number {
    background: var(--green-muted);
    color: #030e08;
  }

  .cycle-step.next-level {
    border-color: rgba(157, 132, 245, 0.4);
    background: rgba(8, 7, 28, 0.9);
    animation: subtlePulse 3.5s ease-in-out infinite alternate;
  }

  .cycle-step.next-level .step-number {
    background: var(--text-primary);
    color: #0a0820;
  }

  @keyframes subtlePulse {
    0% { box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3); }
    100% { box-shadow: 0 4px 22px rgba(157, 132, 245, 0.2); }
  }

  .cycle-arrow {
    color: var(--accent-dim);
    font-size: 1.2rem;
    opacity: 0.7;
    animation: arrowPulse 2.5s ease-in-out infinite;
  }

  @keyframes arrowPulse {
    0%, 100% { opacity: 0.35; }
    50% { opacity: 0.85; }
  }

  .loop-indicator {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    padding: 0.9rem 1.4rem;
    background: var(--accent-faint);
    border: 1px solid var(--border-subtle);
    border-radius: var(--radius-sm);
  }

  .loop-arrow {
    font-size: 1.4rem;
    color: var(--accent);
    animation: loopSpin 5s linear infinite;
    flex-shrink: 0;
  }

  @keyframes loopSpin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }

  .loop-text {
    color: var(--text-secondary);
    font-size: 0.88rem;
    font-style: italic;
  }

  @media (max-width: 768px) {
    .cycle-row {
      flex-direction: column;
      gap: 1rem;
    }

    .cycle-arrow {
      transform: rotate(90deg);
    }

    .cycle-step {
      min-width: 90%;
    }

    .recipe-section {
      padding: var(--space-xl) var(--space-md);
    }

    .loop-indicator {
      flex-direction: column;
      text-align: center;
    }
  }
</style>

<div class="recipe-section">

  <div class="recipe-content">
    <div class="level-system">
      <div class="level-indicator">
        <div class="level-bar">
          <div class="level-progress"></div>
        </div>
        <span class="level-text">LVL ∞</span>
      </div>

      <div class="cycle-container">
        <div class="cycle-row">
          <div class="cycle-step">
            <div class="step-number">1</div>
            <div class="step-icon">⚔️</div>
            <div class="step-text">Challenge</div>
            <div class="step-desc">Face the hard things</div>
          </div>
          <div class="cycle-arrow">→</div>
          <div class="cycle-step damage">
            <div class="step-number">2</div>
            <div class="step-icon">💔</div>
            <div class="step-text">Break</div>
            <div class="step-desc">Get damaged, fail</div>
          </div>
          <div class="cycle-arrow">→</div>
          <div class="cycle-step">
            <div class="step-number">3</div>
            <div class="step-icon">🛌</div>
            <div class="step-text">Recover</div>
            <div class="step-desc">Rest and heal</div>
          </div>
        </div>

        <div class="cycle-row">
          <div class="cycle-step growth">
            <div class="step-number">4</div>
            <div class="step-icon">🌱</div>
            <div class="step-text">Growth</div>
            <div class="step-desc">Adapt and learn</div>
          </div>
          <div class="cycle-arrow">→</div>
          <div class="cycle-step">
            <div class="step-number">5</div>
            <div class="step-icon">⬆️</div>
            <div class="step-text">Level Up</div>
            <div class="step-desc">Become stronger</div>
          </div>
          <div class="cycle-arrow">→</div>
          <div class="cycle-step next-level">
            <div class="step-number">6</div>
            <div class="step-icon">⚔️</div>
            <div class="step-text">Harder Challenge</div>
            <div class="step-desc">Repeat at higher level</div>
          </div>
        </div>
      </div>

      <div class="loop-indicator">
        <span class="loop-arrow">↻</span>
        <span class="loop-text">The cycle continues — each time you're stronger than before</span>
      </div>
    </div>
  </div>
</div>
