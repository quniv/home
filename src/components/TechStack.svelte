<style>
  .tech-strip {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 1.5rem;
    padding: 2rem 0;
    flex-wrap: wrap;
  }

  .icon-wrap {
    width: 64px;
    height: 64px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid rgba(0, 245, 255, 0.15);
    border-radius: 4px;
    background: rgba(0, 245, 255, 0.03);
    color: rgba(0, 245, 255, 0.45);
    transition: all 0.3s ease;
  }

  .icon-wrap:hover {
    border-color: rgba(0, 245, 255, 0.5);
    background: rgba(0, 245, 255, 0.07);
    color: #00f5ff;
    box-shadow: 0 0 20px rgba(0, 245, 255, 0.15);
    transform: translateY(-3px);
  }

  .icon-wrap svg {
    width: 32px;
    height: 32px;
  }

  .icon-wrap img {
    width: 32px;
    height: 32px;
    opacity: 0.45;
    transition: opacity 0.3s ease;
  }

  .icon-wrap:hover img {
    opacity: 1;
  }
</style>

<div class="tech-strip">
  <!-- Kubernetes -->
  <div class="icon-wrap">
    <img src="https://cdn.simpleicons.org/kubernetes/00f5ff" alt="" />
  </div>

  <!-- AWS -->
  <div class="icon-wrap">
    <img src="https://cdn.simpleicons.org/amazonwebservices/00f5ff" alt="" />
  </div>

  <!-- IoT: connected triangle nodes -->
  <div class="icon-wrap">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round">
      <circle cx="12" cy="4" r="2" fill="currentColor" stroke="none" />
      <circle cx="4" cy="19" r="2" fill="currentColor" stroke="none" />
      <circle cx="20" cy="19" r="2" fill="currentColor" stroke="none" />
      <line x1="12" y1="6" x2="5.7" y2="17.3" />
      <line x1="12" y1="6" x2="18.3" y2="17.3" />
      <line x1="6" y1="19" x2="18" y2="19" />
    </svg>
  </div>

  <!-- AI: 3-layer neural network -->
  <div class="icon-wrap">
    <svg viewBox="0 0 24 24" fill="currentColor" stroke="none">
      <circle cx="3" cy="8" r="1.5" />
      <circle cx="3" cy="16" r="1.5" />
      <circle cx="12" cy="5" r="1.5" />
      <circle cx="12" cy="12" r="1.5" />
      <circle cx="12" cy="19" r="1.5" />
      <circle cx="21" cy="9" r="1.5" />
      <circle cx="21" cy="15" r="1.5" />
      <g stroke="currentColor" stroke-width="1" fill="none" opacity="0.7">
        <line x1="4.5" y1="8" x2="10.5" y2="5.5" />
        <line x1="4.5" y1="8" x2="10.5" y2="12" />
        <line x1="4.5" y1="16" x2="10.5" y2="12" />
        <line x1="4.5" y1="16" x2="10.5" y2="18.5" />
        <line x1="13.5" y1="5.5" x2="19.5" y2="9" />
        <line x1="13.5" y1="12" x2="19.5" y2="9" />
        <line x1="13.5" y1="12" x2="19.5" y2="15" />
        <line x1="13.5" y1="18.5" x2="19.5" y2="15" />
      </g>
    </svg>
  </div>

  <!-- Quantum: atom with 3 orbital ellipses -->
  <div class="icon-wrap">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
      <circle cx="12" cy="12" r="1.8" fill="currentColor" stroke="none" />
      <ellipse cx="12" cy="12" rx="10" ry="3.5" />
      <ellipse cx="12" cy="12" rx="10" ry="3.5" transform="rotate(60 12 12)" />
      <ellipse cx="12" cy="12" rx="10" ry="3.5" transform="rotate(-60 12 12)" />
    </svg>
  </div>

  <!-- Robotics: robot head -->
  <div class="icon-wrap">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round">
      <rect x="5" y="9" width="14" height="10" rx="1.5" />
      <rect x="9" y="5" width="6" height="4" rx="1" />
      <line x1="12" y1="5" x2="12" y2="9" />
      <circle cx="9" cy="13.5" r="1.5" fill="currentColor" stroke="none" />
      <circle cx="15" cy="13.5" r="1.5" fill="currentColor" stroke="none" />
      <line x1="9" y1="17" x2="15" y2="17" />
      <line x1="2.5" y1="12" x2="5" y2="12" />
      <line x1="19" y1="12" x2="21.5" y2="12" />
    </svg>
  </div>
</div>
