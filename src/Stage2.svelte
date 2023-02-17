<script>
    import { createEventDispatcher } from "svelte";
    import CreateHabit from "./lib/Stage2/CreateHabit.svelte";

    const dispatch = createEventDispatcher();

    let habits = JSON.parse(localStorage.getItem("habits"));
    if (!habits) {
        habits = [];
        // localStorage.setItem("habits", JSON.stringify(habits));
    }

    let creatingHabit = false;
    const onOpenCreate = () => creatingHabit = true;

    const onClose = () => creatingHabit = false;

    const addHabit = (name, value) => {
      // console.log(`Adding habit: ${name}`)
      habits.push({name: name, value: value});
      habits = habits;
      // localStorage.setItem("habits", JSON.stringify(habits));
    }

    const onCloseCreate = (event) => {
    //   console.log(`recieved dispatch to add habit: ${event.detail.name}`)
      creatingHabit = false;
      let error = false;
      habits.forEach(habit => {
        if (habit.name == event.detail.name) {
          dispatch('createError', {message: "Habit already exists"})
          error=true;
        }
      });
      if (!error){
        addHabit(event.detail.name, event.detail.value);
      }
    }

</script>

<main>
    <h1>Stage 2</h1>
    <p id="instructions">
      Create and track your habits here optionally choose to add a habit template(s)
    </p>
    <button on:click={onOpenCreate} type="button" class="btn btn-primary">New Habit</button>
    <CreateHabit open={creatingHabit} onClosed={onClose} on:addHabit={onCloseCreate}/>
</main>
<style>
  #instructions {
    padding-top: 10px;
    padding-left: 12%;
    padding-right: 12%;
    text-align: left;
  }
</style>