<!-- src/App.svelte — Root layout -->
<script>
  import Sidebar from './components/Sidebar.svelte';
  import Starfield from './components/Starfield.svelte';
  import Home from './pages/Home.svelte';
  import Work from './pages/Work.svelte';
  import Services from './pages/Services.svelte';
  import Team from './pages/Team.svelte';
  import Blog from './pages/Blog.svelte';

  let activeTab = 'home';
</script>

<style>
  /* ═══════════════════════════════════════════
     DESIGN TOKENS — Space/Universe palette
     Muted, professional, WCAG-AA grounded
     ═══════════════════════════════════════════ */
  :global(:root) {
    /* Background & surfaces */
    --bg:              #050510;
    --surface:         rgba(8, 6, 28, 0.94);
    --surface-hover:   rgba(14, 11, 40, 0.97);
    --surface-raised:  rgba(11, 9, 34, 0.96);

    /* Borders */
    --border:          rgba(148, 120, 230, 0.2);
    --border-active:   rgba(157, 132, 245, 0.55);
    --border-subtle:   rgba(148, 120, 230, 0.12);

    /* Accent — muted lavender (≈ #9d84f5) */
    --accent:          #9d84f5;
    --accent-dim:      rgba(157, 132, 245, 0.55);
    --accent-faint:    rgba(157, 132, 245, 0.08);
    --accent-faint-md: rgba(157, 132, 245, 0.14);

    /* Secondary accents — desaturated */
    --gold:            #c9991f;
    --pink:            #c95d9a;
    --green-muted:     #4caf85;

    /* Text hierarchy — all pairs checked against --surface on opaque bg */
    /* #e8e3f8 on #08061c  ≈ 13.8:1  (primary) */
    /* #c0bad8 on #08061c  ≈  8.2:1  (secondary) */
    /* #9d94c4 on #08061c  ≈  4.7:1  (muted — passes AA normal) */
    /* #8e84b2 on #08061c  ≈  4.6:1  (dim — passes AA normal for small text) */
    --text-primary:    #e8e3f8;
    --text-secondary:  #c0bad8;
    --text-muted:      #9d94c4;
    --text-dim:        #8e84b2;

    /* Typography */
    --font-body:  'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    --font-mono:  'JetBrains Mono', 'SF Mono', 'Fira Code', monospace;

    /* Spacing scale */
    --space-xs:   0.25rem;
    --space-sm:   0.5rem;
    --space-md:   1rem;
    --space-lg:   1.5rem;
    --space-xl:   2rem;
    --space-2xl:  3rem;
    --space-3xl:  4rem;

    /* Radius */
    --radius-sm:  3px;
    --radius-md:  6px;
  }

  /* ── Global resets ── */
  :global(body) {
    font-family: var(--font-body);
    margin: 0;
    padding: 0;
    background: var(--bg);
    color: var(--text-primary);
    overflow-x: hidden;
    min-height: 100vh;
    position: relative;
    line-height: 1.6;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  /* Nebula cloud overlay — calmer, less chromatic */
  :global(body::before) {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 70% 50% at 20% 20%, rgba(90, 50, 170, 0.10) 0%, transparent 60%),
      radial-gradient(ellipse 55% 40% at 82% 85%, rgba(190, 140, 30, 0.06) 0%, transparent 55%),
      radial-gradient(ellipse 50% 60% at 85% 25%, rgba(80, 130, 210, 0.07) 0%, transparent 55%),
      radial-gradient(ellipse 45% 55% at 12% 75%, rgba(180, 80, 150, 0.06) 0%, transparent 55%),
      radial-gradient(ellipse 90% 80% at 50% 50%, rgba(30, 12, 65, 0.20) 0%, transparent 70%);
    pointer-events: none;
    z-index: 0;
  }

  :global(*) {
    position: relative;
    z-index: 1;
  }

  /* ── Layout shell ── */
  .app-shell {
    display: flex;
    min-height: 100vh;
  }

  /* Offset for the fixed 220px sidebar */
  .content-area {
    margin-left: 220px;
    flex: 1;
    min-width: 0;
    overflow-y: auto;
  }

  @media (max-width: 768px) {
    .content-area {
      margin-left: 0;
    }
  }
</style>

<Starfield />

<div class="app-shell">
  <Sidebar bind:activeTab />

  <div class="content-area">
    {#if activeTab === 'home'}
      <Home onNavigate={(id) => { activeTab = id; }} />
    {:else if activeTab === 'work'}
      <Work />
    {:else if activeTab === 'services'}
      <Services />
    {:else if activeTab === 'team'}
      <Team />
    {:else if activeTab === 'blog'}
      <Blog />
    {/if}
  </div>
</div>
