<script>
  import { createEventDispatcher } from 'svelte';

  export let open = false;
  export let showBackdrop = true;
  export let onClosed;

  let name;
  let value;

  const dispatch = createEventDispatcher();

  const modalClose = () => {
      open = false;
      name = null;
      value = null;
      if (onClosed) {
          onClosed();
      }
  }

  const modalSave = () => {
    if (name && value) {
        open = false;
        dispatch('addHabit', {name, value})
    }
    name = null;
    value = null;
  }
</script>

{#if open}
<div class="modal" id="sampleModal" tabindex="-1"
  role="dialog" aria-labelledby="sampleModalLabel" aria-hidden={false}
>
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="sampleModalLabel">Add Habit</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"on:click={modalClose}>
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
          <div class="row">
              <div class="col">
                  <input bind:value={name} type="text" class="form-control" placeholder="Habit" aria-label="Habit" aria-describedby="basic-addon1">
              </div>
              <div class="col">
                  <select bind:value={value} class="form-select" aria-label="Default select example">
                      <option disabled selected hidden style="color: #6c757d">Type</option>
                      <option value="+">
                          Positive
                      </option>
                      <option value="*">
                          Neutral
                      </option>
                      <option value="-">
                          Negative
                      </option>
                  </select>
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
</style>