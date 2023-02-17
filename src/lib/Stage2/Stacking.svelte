<script>
    export let name;
    export let habit;
</script>
<main>
    <div class="input-group mb-3">
        <div class="input-group-prepend">
          <span class="input-group-text" id="basic-addon1">After</span>
        </div>
        <input bind:value={habit} type="text" class="form-control" placeholder="Current Habit" aria-label="current habit" aria-describedby="basic-addon1">
        <div class="input-group-append">
            <span class="input-group-text" id="basic-addon2">I will {name}</span>
        </div>
    </div>
</main>