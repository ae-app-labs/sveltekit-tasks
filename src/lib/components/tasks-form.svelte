<script lang="ts">
    let newTask = $state("");
    let { addTask }: {
        addTask: (newTask: string) => void;
    } = $props();

    let formSubmitted = (event:SubmitEvent) => {
        event.preventDefault();
        addTask(newTask);
        newTask = "";
    };
</script>

<form action="" class="form mb-4" onsubmit={formSubmitted}>
    <div class="columns is-vcentered">
        <div class="column">
            <input type="text" id="newTask" name="newTask" class="input is-medium" bind:value={newTask} placeholder="Enter Task Name" />
        </div>
        <div class="column is-narrow">
            <button class="button is-primary is-medium">Add</button>
        </div>
    </div>
</form>
