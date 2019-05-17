<script>
	import CardList from "./components/Card/ListCard.svelte";

	var todos = [];
	var completed = [];
	var newTodo = {
		title: '',
		desc: ''
	};
	function addTodo(e){
		e.preventDefault();
		if(newTodo.title.length){
			var copyTodo = JSON.parse(JSON.stringify(newTodo));
			if(Array.isArray(todos)){
				copyTodo.id = '';
				copyTodo.id = Math.floor(100000 + Math.random() * 900000);
				todos.push(copyTodo);
				todos = todos;
			}
		}
	}
	
	function moveToCompletedTodo(event){
		var id = event.detail.id;
		let currentTodo = todos.filter((item,index) => {
			return (item.id === id) ? true: false;
		});
		completed.push(currentTodo[0]);
		completed = completed;
		removeUncompletedTodo(id);
	}

	function removeUncompletedTodo(id){
		let currentTodo = todos.filter((item,index) => {
			return (item.id === id) ? false: true;
		});
		todos = currentTodo;
	}

	function removeCompletedTodo(event){
		var id = event.detail.id;

		let currentTodo = completed.filter((item,index) => {
			return (item.id === id) ? false: true;
		});
		completed = currentTodo;	
	}
</script>

<style>
	.text-center{
		text-align:center;
	}
	.container{
		width: 80%;
		margin: 0 auto;
	}

	.w-33{
		width: 32%;
		display: flex;
	}
	.flex-row{
		flex-direction: row;
	}
	.flex{
		display: flex;
	}
	.block{
		display: block;
	}
	.space-between{ 
		justify-content: space-between;
	}
</style>

<div class="container">
	<div class="container flex-row flex space-between">
		<CardList on:listclick={moveToCompletedTodo} title="Todo" list={todos} buttonText="completed"/>
		<CardList on:listclick={removeCompletedTodo} title="Completed Todo" list={completed} buttonText="Remove" />
		
		<div class="block">
			<h1>Add A Todo</h1>
			<form on:submit|preventDefault={addTodo}>
				<div class="form-group">
					<label for="title">Title</label>
					<input type="text" name="title" bind:value={newTodo.title}>
				</div>
				<div class="form-group">
					<label for="desc">Description</label>
					<textarea type="text" name="desc" bind:value={newTodo.desc}/>
				</div>
				<div class="form-group">
					<button on:click={addTodo} type="submit">Add A ToDo</button>
				</div>
						
			</form>		
		</div>	
		
	</div>	
</div>
