<script>
  import Form from "./Form.svelte";
  import Imc from "./Imc.svelte";

  const name = "World";

  let poids = 80;
  let taille = 1.8;

  // function computeEvent(e) {
  //   const formData = new FormData(e.target);
  //   poids = parseFloat(formData.get("poids"));
  //   taille = parseFloat(formData.get("taille"));
  // }
</script>

<p>Bonjour {name}</p>
<Form {taille} {poids} />

<Imc {poids} {taille} />
