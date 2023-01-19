
<script>
  export const prerender = true;
  import KeyPad from './lib/KeyPad.svelte';
  import Controls from './lib/Controls.svelte';

  

  let finalText = "";
  let rows = 1;
  let columns = 3;
  const allChars = "ABCDEFGHIJKLMNOPQRSTUVWXYZ ."
  let chars = allChars;
  let visible = true;


  function handleKeyPress(event) {
      visible=false
      setTimeout(()=>{
          if (event.detail.text.length == 1)
          {
              finalText += event.detail.text;
              chars = allChars;
          }
          else
          {
              chars = event.detail.text;
          }  
          visible = true;
      }, 501)
}

  function handleReset()
  {
      chars = allChars;
      finalText = "";
  }
  
</script>
<body>
      
  <KeyPad
  on:keyPress={ handleKeyPress }
  bind:chars={chars}
  bind:rows={rows}
  bind:columns={columns}
  bind:visible={visible}
  />

  <Controls
      bind:finalText={finalText}
      bind:columns={columns}
      bind:rows={rows}
      on:reset={handleReset}
  />

</body>

<style>
  body {
      height: 95vh;
      width: 100vw;
  }
</style>
