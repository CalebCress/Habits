<script>
    import SheetHabit from "./SheetHabit.svelte";
    import Icon from 'svelte-awesome';
    import { plus, minus, asterisk } from 'svelte-awesome/icons';
    let habits = JSON.parse(localStorage.getItem("sheetHabits"));
</script>
<main>
    <div id="tracker">
        <table class="table">
            <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">Daily Habits</th>
                <th scope="col">
                    <span style="color: #198754"><Icon data={plus}/></span>
                    <span style="color: #adb5bd"><Icon data={asterisk}/></span>
                    <span style="color: #dc3545"><Icon data={minus}/></span>
                </th>
            </tr>
            </thead>
            <tbody>
            <SheetHabit row={1} name={"habit1"} value={"+"}/>
            <SheetHabit row={2} name={"habit2"} value={"*"}/>
            <SheetHabit row={3} name={"habit3"} value={"-"}/>
            <tr>
                <th scope="col" colspan="3">
                    <div id="addHabit">
                        Add Habit
                    </div>
                </th>
            </tr>
            </tbody>
        </table>
    </div>
</main>
<style>
    #addHabit:hover {
        cursor: pointer;
        color: grey;
    }
</style>