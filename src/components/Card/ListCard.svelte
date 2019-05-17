<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	
	export var list;
	export var title;
	export var buttonText;
	list = list.length ? list : [];

	function buttonClickEvent(todo){
		dispatch('listclick', {
			id: todo.id,
			todo: todo
		});
	}
</script>

<div class="block">
	<h1 class="text-center">{ title }</h1>
	<ul>
		{#each list as todo}
		<li>
			<div>
				<span>{todo.title}</span>
				<button on:click={() => buttonClickEvent(todo)}>{buttonText}</button>
			</div>
		</li>
		{/each}
	</ul>
</div>