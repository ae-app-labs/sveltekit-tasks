<script lang="ts">
    import TasksForm from "$lib/components/tasks-form.svelte";
    import TasksList from "$lib/components/tasks-list.svelte";
    import type { Filter, Task } from "$lib/types";

    let message = "Tasks App"
    let currentFilter = $state<Filter>("all");
    let tasks = $state<Task[]>([]);

    let totalDone = $derived(tasks.reduce(
        (acc, task) => acc + (task.done ? 1 : 0),
        0
    ));

    let filteredTasks = $derived.by( () => {
        switch (currentFilter) {
            case "all":
                return tasks;
            case "todo":
                return tasks.filter(task => !task.done);
            case "done":
                return tasks.filter(task => task.done);
        }
    })

    function addTask(newTask: string) {
        tasks.push({
            id: crypto.randomUUID(),
            title: newTask,
            done: false
        });
    }

    function toggleDone(task: Task) {
        task.done = !task.done;
    }

    function removeTask(id: string) {
        const index = tasks.findIndex(task => task.id === id);
        tasks.splice(index, 1);
    }

</script>

{#snippet filterButton(filter: Filter)}
    <button class="button is-secondary is-capitalized" 
        onclick={() => currentFilter= filter}>{filter}</button>
{/snippet}

<div class="container">
    <section class="section">
        <h1 class="is-size-2">{message}</h1>
        <TasksForm {addTask} />
    </section>
    <section class="section">
        {#if tasks.length}
            <p>{totalDone} / {tasks.length} tasks completed</p>
            <div class="my-2">
                {@render filterButton("all")}
                {@render filterButton("todo")}
                {@render filterButton("done")}
            </div>
        {:else}
            <p>No tasks yet</p>
        {/if}
        
        <TasksList tasks={filteredTasks} {toggleDone} {removeTask}/>
    </section>
</div>
