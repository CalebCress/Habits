<script>
  import { createEventDispatcher } from "svelte";
  import CreateHabit from "./lib/Stage2/CreateHabit.svelte";

  import { Icon } from "svelte-awesome";
  import chevronLeft from 'svelte-awesome/icons/chevronLeft';
  import chevronRight from 'svelte-awesome/icons/chevronRight';
  import trashO from 'svelte-awesome/icons/trashO'

  import { months } from "./months";

  const dispatch = createEventDispatcher();

  let habits = JSON.parse(localStorage.getItem("habits"));
  if (!habits) {
      habits = [];
      localStorage.setItem("habits", JSON.stringify(habits));
  }
  $: localStorage.setItem("habits", JSON.stringify(habits));
  $: console.log(habits)
  let month =  new Date().getMonth();
  
  let creatingHabit = false;
  const onOpenCreate = () => creatingHabit = true;

  const onClose = () => creatingHabit = false;

  let defaultChecked = []

  months.forEach((m,i) => {
    defaultChecked[i] = Array(m.days).fill(false)
  })

  const addHabit = (name, implementation, stacking) => {
    console.log(`Adding habit: ${name}`)
    habits.push({name, implementation, stacking, check: defaultChecked});
    habits = habits;
    localStorage.setItem("habits", JSON.stringify(habits));
  }

  const onCloseCreate = (event) => {
    console.log(`recieved dispatch to add habit: ${event.detail.name}`)
    creatingHabit = false;
    let error = false;
    habits.forEach(habit => {
      if (habit.name == event.detail.name) {
        dispatch('createError', {message: "Habit already exists"});
        error=true;
      }
    }); 
    if (!error){
      addHabit(event.detail.name, event.detail.implementation, event.detail.stacking);
    }
  }

  const onMonthDown = () => {
    if (month===0) {
      month = 11;
    } else {
      month--;
    }
  }
  const onMonthUp = () => {
    if (month === 11) {
      month = 0;
    } else {
      month++;
    }
  }

  const removeHabit = (habitName) => {
    habits = habits.filter(hab => hab.name !== habitName);
    habits=habits;
    localStorage.setItem("habits", JSON.stringify(habits));
  }

</script>

<main>
    <h1>Stage 2</h1>
    <p id="instructions">
      Create and track your habits here optionally choose to add a habit template(s)
    </p>
    <div class="container text-center" id="monthTitle">
      <div class="row">
        <div class="col-2">
          <button on:click={onMonthDown} class="btn btn-outline-primary btn-sm"><Icon data={chevronLeft}/></button>
        </div>
        <div class="col">
          <h3><span style="cursor: default; vertical-align: auto">{months[month].name}</span></h3>
        </div>
        <div class="col-2">
          <button on:click={onMonthUp} class="btn btn-outline-primary btn-sm"><Icon data={chevronRight}/></button>
        </div>
      </div>
    </div>
    <table class="table-sm">
      <thead>
        <tr>
          <th scope="col">Habit</th>
          {#each Array(months[month].days) as _, i}
            <th scope="col">{i+1}</th>
          {/each}
        </tr>
      </thead>
      <tbody>
          {#each habits as habit, h}
            <tr>
              <th scope="row">{habit.name}</th>
              {#each Array(months[month].days) as _, i}
                <th scope="col"><input bind:checked={habits[h].check[month][i]} class="form-check-input" type="checkbox" value="{i}" id="flexCheckDefault"></th>
              {/each}
              <button on:click={() => { removeHabit(habit.name)}}><span style="color: #dc3545"><Icon data={trashO}/></span></button>
            </tr>
          {/each}
      </tbody>
    </table>
    <button on:click={onOpenCreate} type="button" class="btn btn-primary">New Habit</button>
    <CreateHabit open={creatingHabit} onClosed={onClose} on:createHabit={onCloseCreate}/>
</main>
<style>
  #monthTitle {
    width: 300px;
  }
  #instructions {
    padding-top: 10px;
    padding-left: 12%;
    padding-right: 12%;
    text-align: center;
    /* width: 1000px; */
  }
</style>