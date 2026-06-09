<style>
  .scroll-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: var(--space-2xl) var(--space-xl);
    margin: var(--space-2xl) 0;
  }

  .hanging-scroll {
    display: flex;
    flex-direction: column;
    align-items: center;
    animation: scrollSway 6s ease-in-out infinite;
    filter: drop-shadow(0 6px 18px rgba(0, 0, 0, 0.4));
  }

  @keyframes scrollSway {
    0%, 100% { transform: rotate(-0.8deg); }
    50% { transform: rotate(0.8deg); }
  }

  .scroll-rod {
    width: 120px;
    height: 10px;
    background: linear-gradient(180deg, #1c1a3e 0%, #0e0c2a 50%, #080620 100%);
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.6);
    position: relative;
  }

  .scroll-rod.top::before,
  .scroll-rod.top::after {
    content: '';
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    width: 8px;
    height: 16px;
    background: linear-gradient(180deg, var(--accent) 0%, #6d3fcf 100%);
    border-radius: 1px;
  }

  .scroll-rod.top::before { left: 4px; }
  .scroll-rod.top::after { right: 4px; }

  .scroll-body {
    width: auto;
    background: linear-gradient(180deg, #09082a 0%, #0b0a30 50%, #09082a 100%);
    border-left: 2px solid var(--accent-dim);
    border-right: 2px solid var(--accent-dim);
    padding: 1rem 1.2rem;
    position: relative;
  }

  .scroll-text {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.1rem;
  }

  .scroll-text.two-col {
    flex-direction: row;
    gap: 1rem;
  }

  .scroll-col {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.1rem;
  }

  .scroll-text span {
    font-family: 'Noto Serif SC', 'SimSun', serif;
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--accent);
    transition: color 0.25s ease;
    line-height: 1.2;
  }

  .scroll-text span:hover {
    color: var(--pink);
  }

  .scroll-rod.bottom {
    position: relative;
  }

  .scroll-tassel {
    width: 4px;
    height: 38px;
    background: linear-gradient(180deg, var(--accent-dim), transparent);
    position: relative;
    margin-top: -2px;
  }

  .scroll-tassel::after {
    content: '';
    position: absolute;
    bottom: -18px;
    left: 50%;
    transform: translateX(-50%);
    width: 18px;
    height: 28px;
    background: linear-gradient(180deg, var(--pink) 0%, #a01878 100%);
    clip-path: polygon(50% 0%, 100% 20%, 80% 100%, 20% 100%, 0% 20%);
  }

  @media (max-width: 768px) {
    .hanging-scroll {
      transform: scale(0.82);
    }
  }
</style>

<div class="scroll-section">
  <div class="hanging-scroll">
    <div class="scroll-rod top"></div>
    <div class="scroll-body">
      <div class="scroll-text two-col">
        <div class="scroll-col">
          <span>天</span>
          <span>上</span>
          <span>天</span>
          <span>下</span>
        </div>
        <div class="scroll-col">
          <span>唯</span>
          <span>我</span>
          <span>独</span>
          <span>尊</span>
        </div>
      </div>
    </div>
    <div class="scroll-rod bottom"></div>
    <div class="scroll-tassel"></div>
  </div>

</div>
