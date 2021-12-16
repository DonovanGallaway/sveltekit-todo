<script context='module'>
    import {goto} from '$app/navigation'
    import Form from '../components/Form.svelte'
    
    let url = 'https://dg-todos.herokuapp.com/todos/'
    let postUrl = url
    let todo = {}
    let id;
    let formData = {}

    export async function load({page, fetch}){
        id = page.params.id
        postUrl += id
        const res = await fetch(url)
        const data = await res.json()
        todo = data.find(x => x._id === id)
        formData = todo
        return {
            props: {
                todo
            }
        }
    }

    const deleteTodo = async () => {
        await fetch(url+id, {
            method: "delete"
        })
        goto('/')
    }
    
</script>

<button on:click={deleteTodo}>Delete</button>

{#if !todo.subject}
    <h1>Loading</h1>

{:else if todo}
    <Form method="put" formData={formData} url={postUrl}/>
    <h1>{todo.subject}</h1>
    <h2>{todo.details}</h2>
    {#if todo.done === true}
    <p>Done!</p>
    {:else}
    <p>Still needs doing</p>
    {/if}
{:else}
    <h1>Error Loading Todo</h1>
{/if}
