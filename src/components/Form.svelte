<script>
    export let formData
    export let url
    export let method

    let formStyle = "none"


    /////////////////////////
	// Functions
	/////////////////////////

	const addTodo = async () => {
		await fetch(url, {
			method: "post",
			headers: {
				"Content-Type": "application/json"
			},
			body: JSON.stringify(formData)
		})
	}

    const updateTodo = async () => {
        console.log(formData)
        await fetch(url, {
            method: "put",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify(formData)
        })
    }
</script>

<style>
    form {
        display: var(--form-show)
    }
</style>

{#if method === 'post'}
    <button on:click={() => {formStyle = 'block'}}>Add New Todo</button>
    <form on:submit={addTodo} style="--form-show: {formStyle}">
        <label for="subject">Subject: 
        <input type='text' bind:value={formData.subject} name="subject"/>
        </label>
        <label for="details">Details:
            <input type='text' bind:value={formData.details} name='details'/>
        </label>
        <label for="done">Done?: 
            <input type='checkbox' name='done' bind:checked={formData.done}/>
        </label>
        <input type='submit'/>
    </form>
{:else if method === 'put'}
    <button on:click={() => {formStyle = 'block'}}>Edit Todo</button>
    <form on:submit={updateTodo} style="--form-show: {formStyle}">
        <label for="subject">Subject: 
        <input type='text' bind:value={formData.subject} name="subject"/>
        </label>
        <label for="details">Details:
            <input type='text' bind:value={formData.details} name='details'/>
        </label>
        <label for="done">Done?: 
            <input type='checkbox' name='done' bind:checked={formData.done}/>
        </label>
        <input type='submit'/>
    </form>
{/if}
