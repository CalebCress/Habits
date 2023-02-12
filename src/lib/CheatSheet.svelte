<script>
    import SheetHabit from "./SheetHabit.svelte";
</script>
<main>
    <div id="tracker">
        <table class="table">
            <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">Daily Habits</th>
                <th scope="col">+ - =</th>
            </tr>
            </thead>
            <tbody>
            <SheetHabit row={1}/>
            <SheetHabit row={2}/>
            <SheetHabit row={3}/>
            </tbody>
        </table>
    </div>
</main>
<style>
</style>