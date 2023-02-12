<script>
    import { fade } from "svelte/transition";
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();
    export let message;
    export let id;

    const deleteError = (id) => {
        dispatch('removeError', {id});
    }

    setTimeout(() => {
        deleteError(id);
    }, 3000)

</script>
<main>
    <div class="error">
        <div transition:fade class="insideError alert alert-danger" role="alert">
            {message}
        </div>      
    </div>
</main>
<style>
    .error {
        position: absolute;
        text-align: center;
        margin-left: 50px;
        z-index: 10;
    }
</style>