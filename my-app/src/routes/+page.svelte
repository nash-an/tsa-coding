<div class="w-screen h-screen bg-black py-10">
    <div class="bg-white max-w-xl mx-auto h-full p-5 relative">
        <h1 class="text-3xl text-center pb-5 font-bold">To-Do List</h1>
        <div class="grid grid-cols-1 gap-2 pb-2">
            {#each todos as todo, i}
            <div class="border border-black flex flex-row justify-between bg-gray-300 gap-2 py-6 items-center px-2 relative">
                <div class="flex flex-row">
                    <input bind:checked={todos[i].checked} type="checkbox" class="mx-2"/>
                    <p>{todo.name}</p>
                </div>
                <button class="cursor-pointer text-red-600" on:click={() => {
                    const newarr = [];

                    for (let j = 0; j < todos.length; j++) {
                        if (j != i) {
                            newarr.push(todos[j])
                        }
                    }

                    todos = newarr;

                    localStorage.setItem('todos', JSON.stringify(todos))
                }}>Delete</button>
            </div>
            {/each}
        </div>

        <form on:submit|preventDefault={
            () => {
                todos.push({name: input, checked: false})
                todos = todos
                input = ''
                localStorage.setItem('todos', JSON.stringify(todos))
            }
        }>
            <input bind:value={input} placeholder="Enter your todo..." type="text" class="bg-gray-300 border border-black w-full p-3">
        </form>

    
    </div>
</div>

<script>
	import { onMount } from "svelte";

    let input = ''

    let todos = [
        {
            name: "Wash Dishes",
            checked: true
        },
        {
            name: "Walk Dog",
            checked: true
        },
        {
            name: "Fold Laundry",
            checked: true
        }
    ]

    onMount(() => {
        if (localStorage.getItem('todos')) {
            todos = JSON.parse(localStorage.getItem('todos'))
        }  
    })
</script>