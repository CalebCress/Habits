<script>
    import CheatSheet from "./lib/CheatSheet.svelte";
</script>

<main>
    <h1>Stage 1</h1>
    <p id="instructions">
        Stage 1 takes place over ~2 weeks the purpose is to just get a sense of your current habits.
        To start pay attention to your natural habits every day and log them here as Posotive (+), Negative (-), or Neutral(=).
    </p>
    <CheatSheet/>
</main>
<style>
    #instructions {
        padding-left: 15%;
        padding-right: 15%;
    }
</style>