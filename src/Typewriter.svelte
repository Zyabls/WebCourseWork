<script>
  let fileContent = '';
  export let y = 0;
  export let text = "You are here"; // Default text
  export let isPlayer = false; // Default condition


  
  function typewriter(node, { speed = 1 }) {
      const valid = node.childNodes.length === 1 && node.childNodes[0].nodeType === Node.TEXT_NODE;
  
      if (!valid) {
        throw new Error(`This transition only works on elements with a single text node child`);
      }
  
      const text = node.textContent;
      //const duration = text.length / (speed * 0.6);
      const duration = text.length / (speed * 0.06);
  
      return {
        duration,
        tick: (t) => {
          const i = ~~(text.length * t);
          node.textContent = text.slice(0, i);
        }
      };
    }
    
  </script>
  
  
  {#if y<500 && isPlayer}
    <p transition:typewriter>{text}</p>
  {/if}
  {#if y>599 && !isPlayer}
    <p transition:typewriter>{text}</p>
  {/if}
  {#if y>599  && y<650 && !isPlayer}
    <p transition:typewriter>hi hi hi</p>
  {/if}

  