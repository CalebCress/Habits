<script>
  import { createEventDispatcher } from 'svelte';
  import Stacking from './Stacking.svelte';
  import Implementation from './Implementation.svelte';

  export let open = false;
  export let showBackdrop = true;
  export let onClosed;
  let implementation = false;
  let stacking = false;
  let implementationTime = "";
  let implementationLocation = "";
  let stackingHabit = "";

  let name;
  let template;

  const dispatch = createEventDispatcher();

  const modalClose = () => {
      open = false;
      name = null;
      template = "add";
      if (onClosed) {
          onClosed();
      }
  }

  const modalSave = () => {
    open = false;
    name = null;
    template = "add";
    if (name) {
        open = false;
        dispatch('createHabit', {
          name,
          implementation: {
            exists: implementation,
            time: implementationTime,
            location: implementationLocation
          }, stacking: {
            exists: stacking,
            habit: stackingHabit
          }
        })
    }
    name = null;
    implementation = false;
    stacking = false;
    implementationTime = "";
    implementationLocation = "";
    stackingHabit = "";
  }

  const addTemplate = () => {
    if (template = "implementationIntetion") {
      implementation = true;
    } else if (template = "habitStacking") {
      stacking = true;
    }
  }
</script>

{#if open}
<div class="modal" id="sampleModal" tabindex="-1"
  role="dialog" aria-labelledby="sampleModalLabel" aria-hidden={false}>
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="sampleModalLabel">Add Habit</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"on:click={modalClose}>
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <div class="inputRow form-floating">
          <input required bind:value={name} id="name" type="text" class="form-control" placeholder="Habit" aria-label="Habit" aria-describedby="basic-addon1">
          <label for="name">Habit</label>
        </div>
        {#if implementation}
          <div class="inputRow">
            <Implementation name={name} bind:time={implementationTime} bind:location={implementationLocation}/>
          </div>
        {/if}
        {#if stacking}
          <div class="inputRow">
            <Stacking name={name} bind:habit={stackingHabit}/>
          </div>
        {/if}
        <div class="inputRow">
          <div class="input-group mb-3">
            <select bind:value={template} class="form-select" aria-label="Default select example">
              <option value="add" disabled selected>Add Template</option>
              <option value="implementationIntention">Implementation Intention</option>
              <option value="habitStacking">Habit Stacking</option>
            </select>
            <button on:click={addTemplate} class="btn btn-outline-primary" type="button" id="button-addon2">Add Template</button>
          </div>
        </div>  
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss= "modal" on:click={modalClose}>Close</button>
        <button type="button" class="btn btn-primary" on:click={modalSave}>Add Habit</button>
      </div>
    </div>
  </div>
</div>
{#if showBackdrop}
  <div class="modal-backdrop show" />
{/if}
{/if}

<style>
  .modal {
    display: block;
  }
  .inputRow {
    margin:10px;
  }
</style>