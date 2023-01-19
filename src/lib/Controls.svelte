<script>
    export const prerender = true;
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    export let rows;
    export let columns;
    export let finalText;

    function reset(){
        dispatch('reset');
    }

</script>


<div class="controls">
    <input type="text" name="" id="" bind:value={finalText} size="30">
    Columns: <input type="text" name="" id="" bind:value={columns} max=10 size="2">
    Rows: <input type="text" name="" id="" bind:value={rows} max=3 size="2">
    <button on:click={reset}>Reset</button>
</div>

<style>
	.controls {
		position: relative; 
        padding: 10px;
        bottom: 0; 
        width: 100%; 
        height: 50px;
        font-size: 30px;
	}
    input {
        line-height: 35px;
        font-size: 30px;
    }
    button {
        line-height: 35px;
        font-size: 30px;
    }
</style>

