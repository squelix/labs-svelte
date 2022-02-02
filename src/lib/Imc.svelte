<script>
  import { poids, taille, imc } from "./stores";
  import { fly, fade } from "svelte/transition";

  $: thin = $imc < 18;
  $: bold = $imc > 25;
</script>

<svelte:head>
  <title>Votre IMC : {$imc}</title>
</svelte:head>

<p class:thin class:bold>
  Votre IMC ({$poids}/{$taille}<sup>2</sup>) est de {$imc}
</p>

{#if $imc < 18}
  <p class="maigre" in:fly={{ y: 200, duration: 2000 }} out:fade>
    Vous êtes maigre
  </p>
{:else if $imc > 25}
  <p class="surpoids" in:fly={{ y: 200, duration: 2000 }} out:fade>
    Vous êtes en surpoids
  </p>
{:else}
  <p class="svelte" in:fly={{ y: 200, duration: 2000 }} out:fade>
    Vous êtes svelte !
  </p>
{/if}

<style>
  .svelte {
    color: green;
  }

  .surpoids {
    color: red;
  }

  .maigre {
    color: orange;
  }

  .thin {
    font-weight: 200;
    font-size: 0.875rem;
  }

  .bold {
    font-weight: 600;
    font-size: 1.125rem;
  }
</style>
