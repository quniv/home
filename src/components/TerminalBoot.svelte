<script>
  import { onMount } from 'svelte';
  import { bootSequence } from '../data/boot.js';

  let terminalText = '';

  onMount(() => {
    let i = 0;
    const typeWriter = () => {
      if (i < bootSequence.length) {
        // eslint-disable-next-line security/detect-object-injection
        terminalText += bootSequence[i] + '\n';
        i++;
        setTimeout(typeWriter, 800);
      }
    };
    setTimeout(typeWriter, 1000);
  });
</script>

<style>
  .terminal-boot {
    position: fixed;
    top: 20px;
    right: 20px;
    background: var(--surface);
    backdrop-filter: blur(18px);
    -webkit-backdrop-filter: blur(18px);
    border: 1px solid var(--border);
    padding: 14px 18px;
    font-size: 11px;
    font-family: var(--font-mono);
    max-width: 290px;
    white-space: pre-line;
    border-radius: var(--radius-sm);
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
    color: var(--text-muted);
    z-index: 100;
    line-height: 1.7;
  }
</style>

{#if terminalText}
  <div class="terminal-boot">{terminalText}</div>
{/if}
