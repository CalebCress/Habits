<script>
  import { createEventDispatcher } from "svelte";
  import Welcome from "./Welcome.svelte";
  import Stage1 from "./Stage1.svelte";
  import DiscussionQuestions from "./DiscussionQuestions.svelte";
  import Stage2 from "./Stage2.svelte";
  import Error from "./lib/Error.svelte";
  import Nav from "./lib/Nav.svelte";

  const dispatch = createEventDispatcher();

  let currentStage = localStorage.getItem('currentStage');

  if(!currentStage) {
    currentStage = "welcome";
    localStorage.setItem('currentStage', currentStage);
  }

  const setStage = (event) => {
    currentStage = event.detail.stage;
    localStorage.setItem('currentStage', currentStage);
  }

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
  <Nav on:setStage={setStage}/>
  <div id="main">
    <!-- <Nav on:setStage={setStage}/> -->
    {#if currentStage === "welcome"}
      <Welcome on:setStage={setStage}/>
    {:else if currentStage === "stage1"}
      <Stage1 on:createError={createError} on:setStage={setStage}/>
    {:else if currentStage === "discussion"}
      <DiscussionQuestions on:setStage={setStage}/>
    {:else if currentStage === "stage2"}
      <Stage2 on:createError={createError}/>
    {/if}
  </div>
</main>

<style>
  #main {
    position: relative;
    z-index: 0;
  }
</style>
