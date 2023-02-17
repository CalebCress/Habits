<script>
    export let name;
    export let time;
    export let location;
</script>
<main>
    <div class="input-group mb-3">
        <div class="input-group-prepend">
          <span class="input-group-text" id="basic-addon1">I will {name} at</span>
        </div>
        <input bind:value={time} type="text" class="form-control" placeholder="Time" aria-label="time" aria-describedby="basic-addon1">
        <div class="input-group-append">
            <span class="input-group-text" id="basic-addon2">in</span>
        </div>
        <input bind:value={location} type="text" class="form-control" placeholder="Location" aria-label="location" aria-describedby="basic-addon1">
    </div>
</main>