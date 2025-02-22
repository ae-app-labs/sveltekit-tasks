<script lang="ts">
    import type { Task } from "$lib/types";
    import { fade } from "svelte/transition";

    let { 
        tasks,
        toggleDone,
        removeTask,
    }: { 
        tasks: Task[];
        toggleDone: (task: Task) => void;
        removeTask: (id: string) => void;
    } = $props();

</script>

{#each tasks as task}
    <article class="message" transition:fade>
        <div class="message-body">
            <div class="content">
                <div class="columns is-vcentered">
                    <div class="column">
                        <div class="field">
                            <div class="field-label">
                                <input type="checkbox" 
                                onchange={() => toggleDone(task)}
                                class="checkbox" checked={task.done} />
                            </div>
                            <div class="field-body">
                                <div class="field">
                                <p class="title is-4">
                                    <span class:has-text-primary={task.done}>
                                        {task.title}
                                    </span>
                                </p>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="column is-1">
                        <p class="subtitle is-6">{task.done ? "Done" : "Pending"}</p>
                    </div>
                    <div class="column is-1">
                        <button class="is-warning button is-outlined" onclick={ () => removeTask(task.id)}>Remove</button>
                    </div>
                </div>
            </div>
        </div>
    </article>
{/each}
