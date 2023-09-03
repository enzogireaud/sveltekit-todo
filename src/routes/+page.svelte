<script lang="ts">
	interface task {
		content: string;
		isEditing: boolean;
		isChecked: boolean;
	}

	let ToDoList: Array<task> = [];
	let inputContent = '';

	function addToDo() {
		ToDoList = [
			...ToDoList,
			{
				content: inputContent,
				isEditing: false,
				isChecked: false
			}
		];
		inputContent = '';
	}

	function edit(i: number, isEditing: boolean) {
		ToDoList[i].isEditing = isEditing;
	}

	function deleteTask(i: number) {
		ToDoList.splice(i, 1);
		ToDoList = ToDoList;
	}
</script>

<h1>To do App</h1>

<intro>
	<p>Enter your to do here :</p>
	<input
		type="text"
		bind:value={inputContent}
		on:keypress={(e) => {
			if (e.key == 'Enter') {
				addToDo();
			}
		}}
	/>
	<button on:click={addToDo}>Add To Do</button>
</intro>
<container>
	{#each ToDoList as task, i}
		<div class="todo">
			{#if task.isEditing}
				<input type="text" bind:value={task.content} />
				<button
					on:click={() => {
						edit(i, false);
					}}>Save</button
				>
			{:else}
				<input type="checkbox" bind:checked={task.isChecked} />
				<h3>{task.content}</h3>
				<button
					on:click={() => {
						edit(i, true);
					}}>Edit</button
				>
			{/if}
			<button on:click={() => deleteTask(i)}>Delete</button>
		</div>
	{/each}
</container>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
	:global(body) {
		text-align: center;
		background: url('bg.jpeg') center/cover;
		background-repeat: no-repeat;
		height: 100vh;
		overflow: hidden;
		font-family: 'Press Start 2P', cursive;
	}
	h1 {
		margin-top: 200px;
	}
	input {
		background: none;
		border: 1px solid black;
		padding: 15px;
		border-radius: 5px;
	}
	button {
		padding: 15px;
		background: none;
		border: 1px solid black;
		border-radius: 3px;
		cursor: pointer;
		transition: 0.2s ease;
		min-width: 70px;
	}
	button:hover {
		background: #000;
		color: white;
	}
	container {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
	}
	.todo {
		justify-content: space-between;
		margin: 10px 0;
		display: flex;
		gap: 20px;
		opacity: 0;
		animation: fadeIn 1s ease forwards;
	}

	@keyframes fadeIn {
		0% {
			opacity: 0;
			filter: blur(5px);
			transform: translateY(50px);
		}
		100% {
			opacity: 1;
			filter: blur(0px);
			transform: translateY(0);
		}
	}
</style>
