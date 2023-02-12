<script>
    import { createEventDispatcher } from "svelte";

    import SheetHabit from "./SheetHabit.svelte";
    import Icon from 'svelte-awesome';
    import { plus, minus, asterisk } from 'svelte-awesome/icons';
    import AddHabit from "./AddHabit.svelte";

    const dispatch = createEventDispatcher();

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

    const removeHabit = (event) => {
        habits.filter(hab => hab.name !== event.details.name);
    }

    let addingHabit = false;

    const onOpenAdd = () => addingHabit = true;

    const onClose = () => addingHabit = false;

    const onCloseAdd = (event) => {
        addingHabit = false;
          let error = false;
          habits.forEach(habit => {
            if (habit.name == event.details.name) {
              dispatch('createError', {message: "Habit already exists"})
              error=true;
            }
          });
          if (!error){
            addHabit(event.details.name, event.details.value);
          }
  }
</script>
<main>
    <div id="tracker">
        <table class="table table-condensed">
            <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">Daily Habits</th>
                <th scope="col">
                  Type
                    <!-- <span style="color: #198754"><Icon data={plus}/></span>
                    <span style="color: #adb5bd"><Icon data={asterisk}/></span>
                    <span style="color: #dc3545"><Icon data={minus}/></span> -->
                </th>
            </tr>
            </thead>
            <tbody>
              {#each habits as {name, value}, i}
              <SheetHabit row={i+1} name={name} value={value}/>
              {/each}
            <tr>
                <th scope="col" colspan="4">
                  <button on:click={onOpenAdd} type="button" class="btn btn-outline-primary">Add Habit</button>
                </th>
            </tr>
            </tbody>
        </table>
    </div>
    <AddHabit open={addingHabit} onClosed={onClose} />
</main>
<style>
</style>