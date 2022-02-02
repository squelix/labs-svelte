<script context="module">
  /** @type {import('@sveltejs/kit').Load} */
  export async function load({ fetch }) {
    const url = `/recettes.json`;
    const res = await fetch(url);

    if (res.ok) {
      return {
        props: {
          recettes: await res.json(),
        },
      };
    }

    return {
      status: res.status,
      error: new Error(`Could not load ${url}`),
    };
  }
</script>

<script>
  export let recettes = [];
</script>

<section class="recettes">
  {#each recettes as recette, index}
    <article>
      <div>
        <h2>
          <a sveltekit:prefetch href="/recettes/{index}">{recette.name}</a>
        </h2>
        <p>
          ⏱ {recette.totalTime} min 👨‍🍳 {[
            "",
            "Très Facile",
            "Facile",
            "Moyenne",
            "Difficile",
          ][recette.difficulty || 0]} € {[
            "",
            "Bon marché",
            "Moyen",
            "Assez cher",
          ][recette.budget || 0]} 😋 {recette.people} Personnes
        </p>
      </div>
      <img src={recette.image} alt="Photo de la recette {recette.name}" />
    </article>
  {/each}
</section>
