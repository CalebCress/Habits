<script>
    import SheetHabit from "./SheetHabit.svelte";
    import Icon from 'svelte-awesome';
    import { plus, minus, asterisk } from 'svelte-awesome/icons';
    import AddHabit from "./AddHabit.svelte";

    let habits = JSON.parse(localStorage.getItem("sheetHabits"));
    if (!habits) {
        habits = [];
        localStorage.setItem("sheetHabits", JSON.stringify(habits));
    }
    
    const addHabit = (name, value) => {
        habits.push({name: name, value: value});
        habits = habits;
        localStorage.setItem("sheetHabits", JSON.stringify(habits));
    }

    

    let addingHabit = false;

    const onOpenAdd = () => addingHabit = true;

    const onCloseAdd = (data) => {
        addingHabit = false;
        if (data) {
          addHabit(data.name, data.value);
        }
    }

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
              {#each habits as {name, value}, i}
              <SheetHabit row={i+1} name={name} value={value}/>
              {/each}
            <tr>
                <th scope="col" colspan="3">
                  <button on:click={onOpenAdd} type="button" class="btn btn-outline-primary">Add Habit</button>
                </th>
            </tr>
            </tbody>
        </table>
    </div>
    <AddHabit open={addingHabit} onClosed={onCloseAdd}/>
</main>
<style>
</style>