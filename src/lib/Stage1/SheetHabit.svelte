<script>
    import { createEventDispatcher } from 'svelte';

    import Icon from 'svelte-awesome';
    import { plus, minus, asterisk, trashO } from 'svelte-awesome/icons';
    export let row;
    export let name;
    export let value;

    const dispatch = createEventDispatcher();

    const remove = () => {
        dispatch('removeHabit', {name})
    }

</script>
<tr>
    <th scope="row">{row}</th>
    <td>{name}</td>
    <td id="value">
        {#if value=="+"}
            <span style="color: #198754"><Icon data={plus}/></span>
        {:else if value=="*"}
            <span style="color: #adb5bd"><Icon data={asterisk}/></span>
        {:else if value=="-"}
            <span style="color: #dc3545"><Icon data={minus}/></span>
        {/if}
    </td>
    <td>
        <button on:click={remove}><span style="color: #dc3545"><Icon data={trashO}/></span></button>
    </td>
</tr>
<style>
    #value {
        font-weight: 900;
        color: green;
    }
</style>