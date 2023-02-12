<script>
  import Stage1 from "./Stage1.svelte";
  import Error from "./lib/Error.svelte";

  let errors = [];
  let errorIdIncrement = 0;

  const createError = (event) => {
    console.log(`error: ${event.detail.message}`)
    errors.push({message: event.detail.message, id: errorIdIncrement})
    errors = errors;
    errorIdIncrement++;
  }

  const removeError = (event) => {
    errors = errors.filter(err => err.id !== event.detail.id);
  }
</script>

<main>
  {#each errors as error}
    <Error on:removeError={removeError} message={error.message} id={error.id}/>
  {/each}
  <div id="main">
    <Stage1 on:createError={createError}/>
  </div>
</main>

<style>
  #main {
    position: relative;
    z-index: 0;
  }
</style>
