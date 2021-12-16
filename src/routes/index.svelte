<script>
	import {onMount} from 'svelte'
	import Form from '../components/Form.svelte'

	let todos = []
	const url = 'https://dg-todos.herokuapp.com/todos/'
	let formData = {
        subject: "",
        details: "",
        done: false
    };

	/////////////////////////
	// On Mount
	/////////////////////////

	onMount(async () => {
		const response = await fetch(url)
		todos = await response.json()
	})
</script>

<h1>Welcome to the To Dos App</h1>
<Form formData={formData} method="post" url={url}/>

{#each todos as todo}
	<a href={`/${todo._id}`}><h1>{todo.subject}</h1></a>
{:else}
	<h1>Loading...</h1>
{/each}