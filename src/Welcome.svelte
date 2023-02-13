<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    const toStage2 = () => {
        dispatch('setStage', {stage: 'stage2'});
    }

    const toStage1 = () => {
        dispatch('setStage', {stage: 'stage1'});
    }
</script>

<main>
    <h1>Welcome!</h1>
    <p id="instructions">
        This is a small web app I created to help implementing the practices in atomic habits.
        It is <b>important</b> you have or are reading atomic habits in order to use this app.
        This app aims to provide a digital place to use the framework in Atomic Habits.
        It does not teach how to effectively develop habits.
        If you have finished Atomic Habits and already are working on your I would reccomend fast forwarding to the end with the button below.
    </p>
    <button on:click={toStage1} class="btn btn-primary">Get Started</button>
    <button on:click={toStage2} class="btn btn-success">I have my own atomic habits</button>
</main>
<style>
    #instructions {
        padding-left: 12%;
        padding-right: 12%;
    }
</style>