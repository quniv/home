<script>
  let lightboxSrc = null;
  let lightboxAlt = '';

  function openLightbox(src, alt) {
    lightboxSrc = src;
    lightboxAlt = alt;
  }

  function closeLightbox() {
    lightboxSrc = null;
  }

  function handleLightboxKey(e) {
    if (e.key === 'Escape') closeLightbox();
  }
</script>

<style>
  .motivation-section {
    background: var(--surface-raised);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    border: 1px solid var(--border);
    margin: var(--space-2xl) 0;
    padding: var(--space-xl) var(--space-xl);
    border-radius: var(--radius-md);
    box-shadow: 0 4px 28px rgba(0, 0, 0, 0.35);
    position: relative;
    overflow: hidden;
  }

  .motivation-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
    gap: 1.25rem;
    margin: 0;
  }

  .gif-card {
    position: relative;
    aspect-ratio: 1;
    overflow: hidden;
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    background: #000;
    transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
    padding: 0;
    cursor: zoom-in;
  }

  .gif-card img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: filter 0.3s ease, transform 0.3s ease;
    filter: saturate(0.8) brightness(0.8);
    display: block;
  }

  .gif-card:hover {
    transform: translateY(-3px);
    border-color: var(--border-active);
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.5);
  }

  .gif-card:hover img {
    filter: saturate(1.1) brightness(1.0);
  }

  .gif-card:focus-visible {
    outline: 2px solid var(--accent);
    outline-offset: 2px;
  }

  /* ── Lightbox ── */
  .lightbox-overlay {
    position: fixed;
    inset: 0;
    z-index: 9999;
    background: rgba(2, 2, 12, 0.94);
    display: flex;
    align-items: center;
    justify-content: center;
    animation: lb-in 0.18s ease;
  }

  @keyframes lb-in {
    from { opacity: 0; }
    to   { opacity: 1; }
  }

  .lightbox-overlay img {
    max-width: 90vw;
    max-height: 90vh;
    object-fit: contain;
    border: 1px solid var(--border);
    box-shadow: 0 8px 60px rgba(0, 0, 0, 0.7);
    border-radius: var(--radius-sm);
    animation: lb-scale 0.22s cubic-bezier(0.34, 1.56, 0.64, 1);
  }

  @keyframes lb-scale {
    from { transform: scale(0.87); opacity: 0; }
    to   { transform: scale(1);    opacity: 1; }
  }

  .lightbox-close {
    position: fixed;
    top: 1.25rem;
    right: 1.5rem;
    background: var(--surface);
    border: 1px solid var(--border-active);
    color: var(--accent);
    font-size: 1.1rem;
    line-height: 1;
    padding: 0.4rem 0.65rem;
    cursor: pointer;
    border-radius: var(--radius-sm);
    transition: background 0.18s, border-color 0.18s;
  }

  .lightbox-close:hover {
    background: var(--accent-faint-md);
    border-color: var(--accent);
  }

  .lightbox-close:focus-visible {
    outline: 2px solid var(--accent);
    outline-offset: 2px;
  }

  @media (max-width: 768px) {
    .motivation-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 480px) {
    .motivation-grid {
      grid-template-columns: 1fr;
    }
  }
</style>

<div class="motivation-section">
  <div class="motivation-grid">
    <button type="button" class="gif-card" on:click={() => openLightbox('images/medium-mike-tyson-boxer-wallpaper-poster-print-poster-on-13x19-original-imagc5ytjxqtnfur.webp', 'Mike Tyson')}>
      <img src="images/medium-mike-tyson-boxer-wallpaper-poster-print-poster-on-13x19-original-imagc5ytjxqtnfur.webp" alt="Mike Tyson" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/cyberpunk.jpeg', 'Cyberpunk')}>
      <img src="images/cyberpunk.jpeg" alt="Cyberpunk" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/Rosa_Walton_I_Really_Want_to_Stay_at_Your_House.jpg', 'Edgerunners')}>
      <img src="images/Rosa_Walton_I_Really_Want_to_Stay_at_Your_House.jpg" alt="Edgerunners" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/mad.jpg', 'Motivation')}>
      <img src="images/mad.jpg" alt="Motivation" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/unnamed.png', 'Motivation')}>
      <img src="images/unnamed.png" alt="Motivation" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/ranger_training.png', 'Ranger Training')}>
      <img src="images/ranger_training.png" alt="Ranger Training" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/fearless.png', 'Fearless')}>
      <img src="images/fearless.png" alt="Fearless" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/seven_kings_must_die.png', 'Seven Kings Must Die')}>
      <img src="images/seven_kings_must_die.png" alt="Seven Kings Must Die" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/valhalla.png', 'Valhalla')}>
      <img src="images/valhalla.png" alt="Valhalla" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/vikings.png', 'Vikings')}>
      <img src="images/vikings.png" alt="Vikings" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/ninja.png', 'Ninja')}>
      <img src="images/ninja.png" alt="Ninja" />
    </button>
    <button type="button" class="gif-card" on:click={() => openLightbox('images/ironman.png', 'Iron Man')}>
      <img src="images/ironman.png" alt="Iron Man" />
    </button>
  </div>
</div>

{#if lightboxSrc}
  <div class="lightbox-overlay" on:click={closeLightbox} on:keydown={handleLightboxKey} role="dialog" aria-modal="true" tabindex="-1">
    <div on:click|stopPropagation role="presentation"><img src={lightboxSrc} alt={lightboxAlt} /></div>
    <button class="lightbox-close" on:click={closeLightbox} aria-label="Close">✕</button>
  </div>
{/if}
