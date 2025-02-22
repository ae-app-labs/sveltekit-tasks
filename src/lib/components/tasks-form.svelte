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

<form action="" class="form" onsubmit={formSubmitted}>
    <label for="newTask" class="label">
        Task
        <input type="text" id="newTask" name="newTask" class="input is-medium" bind:value={newTask} />
    </label>
    <div class="has-text-right">
        <button class="button is-primary is-medium">Add</button>
    </div>
</form>
