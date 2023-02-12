<script>
    import Icon from 'svelte-awesome';
    import { plus, minus, asterisk } from 'svelte-awesome/icons';
    export let row;
    export let name;
    export let value;
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
</tr>
<style>
    #value {
        font-weight: 900;
        color: green;
    }
</style>