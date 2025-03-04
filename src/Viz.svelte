<script>
  import Header from './template/Header.svelte';
  let { radius, stroke, color, title, subtitle } = $props();

  let width = $state(500); // Default values
  let height = $state(500);

  // Layout
  let headerHeight = $state();

  let vizHeight = $derived(height - headerHeight);
  let vizWidth = $state();
</script>

<svelte:window bind:innerWidth={width} bind:innerHeight={height} />

<div class="chart-container">
  <div class="header-container" bind:clientHeight={headerHeight}>
    {#if title || subtitle}
      <Header {title} {subtitle}></Header>
    {/if}
  </div>
</div>

<div class="viz-container" bind:clientWidth={vizWidth}>
  <svg width={vizWidth} height={vizHeight}>
    <circle
      cx={width / 2}
      cy={height / 2}
      r={radius}
      fill={color}
      stroke="black"
      stroke-width={stroke}
    ></circle>
  </svg>
</div>
