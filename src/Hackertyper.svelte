<script>
  let code = '';

  function handleKeyPress(event) {
    const key = event.key;

    if (key === 'Backspace') {
      code = code.slice(0, -1);
    } else if (/^[a-zA-Z0-9]$/.test(key)) {
      code += key;
    }

    updateCode(code);
  }

  function updateCode(newCode) {
    code = newCode;
    setTimeout(() => {
      updateCode('');
    }, 1000);
  }

  onMount(() => {
    window.addEventListener('keydown', handleKeyPress);
  });

  onDestroy(() => {
    window.removeEventListener('keydown', handleKeyPress);
  });
</script>

<style>
  .terminal {
    font-family: 'Hack', monospace;
    font-size: 14px;
    line-height: 1.5;
    color: #333;
    background-color: #f5f5f5;
    height: 1000px;
  }
</style>

<div class="terminal">
  <span>{code}</span>
</div>