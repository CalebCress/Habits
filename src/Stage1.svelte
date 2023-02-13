<script>
    import { createEventDispatcher } from "svelte";
    import CheatSheet from "./lib/Stage1/CheatSheet.svelte";
    import Icon from 'svelte-awesome';
    import { plus, minus, asterisk } from 'svelte-awesome/icons';

    const dispatcher = createEventDispatcher();
    const toDiscussion = () => {
        dispatcher('setStage', {stage: 'discussion'})
    }
</script>

<main>
    <h1>Stage 1</h1>
    <p id="instructions">
        Stage 1 takes place over ~2 weeks the purpose is to just get a sense of your current habits.
        To start pay attention to your natural habits every day and log them here as one of three types:
        Positive (<span style="color: #198754"><Icon data={plus}/></span>),
        Neutral(<span style="color: #adb5bd"><Icon data={asterisk}/></span>),
        or Negative (<span style="color: #dc3545"><Icon data={minus}/></span>).
    </p>
    <CheatSheet on:createError/>
    <div id="next">
        <button class="btn btn-primary" on:click={toDiscussion}>Next</button>
    </div>
</main>
<style>
    #instructions {
        padding-left: 12%;
        padding-right: 12%;
    }
    #next {
        text-align: right;
    }

</style>