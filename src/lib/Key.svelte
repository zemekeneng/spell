<script>
    export const prerender = true;
    import { createEventDispatcher } from 'svelte';
    export let char;
    const dispatch = createEventDispatcher();

    function addNewLines(chunk){
        let str = ''
        for (let i = 0; i < chunk.length; i++) {
            str += chunk[i];
            if (i%2 == 1 ) {
                str += "<br>";
            }
        }
        return ("<span>" + str + "</span>").replace(" ", "_")
    }

    function keyPress() {
		dispatch('keyPress', {
			text: char
		});
	}
</script>

<button on:click={keyPress}>
    {@html addNewLines(char)}
</button>

<style>
    button {
        font-size: 10em;
    }
</style>

