<script>
    export const prerender = true;
    import Key from './Key.svelte';
    import { fly, fade } from 'svelte/transition';

    export let chars;
    export let rows;
    export let columns;
    export let visible;

    let chunks = new Array();
    
    function chunkSubstr(str, numchks) {
        const chks = [];
        const chkSize = Math.ceil(str.length / Math.floor(numchks))

        for (let i = 0, o = 0; i <= numchks; ++i, o += chkSize) {
            if (str.substr(o, chkSize) != ''){
                chks[i] = str.substr(o, chkSize)
            }
        }
        return chks
    }
    let cells;
    $: cells = rows * columns;
    $: chunks = chunkSubstr(chars, cells);

    let display_columns;
    $:  display_columns = chunks.length > columns ? columns : chunks.length;



</script>
{#if visible}
<div 
    class="keypad" 
    style="--rows:{rows}; --columns:{display_columns};"
    in:fly="{{ y: -200, duration: 500 }}"
    out:fade>
    {#each chunks as ch}
	    <Key on:keyPress char={ch}/>
    {/each}
</div>
{/if}

<style>
	.keypad {
		display: grid;
		grid-template-columns: repeat(var(--columns), auto);
		grid-template-rows: repeat(var(--rows), auto);
		grid-gap: 0.5em;
        height: 100%;
        width: 100%;
	}
</style>

