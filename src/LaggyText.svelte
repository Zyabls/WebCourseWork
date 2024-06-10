<script>
    let y;
    let fileContent = '';
    let splitContent = [];
    let originalWords = [];
  
    let modificationCount = 0;
    let interval; // Define interval variable
  
    fetch('secret.txt')
      .then(response => response.text())
      .then(data => {
        fileContent = data;
        splitContent = fileContent.split(' ');
        originalWords = [...splitContent]; // Store the original words
        updateSplitContent(); // Update splitContent initially
      });
  
    $: updateSplitContent(); // Update splitContent whenever y changes
  
    function updateSplitContent() {
      clearInterval(interval); // Clear the previous interval
  
      interval = setInterval(() => {
        splitContent = modifyWords(splitContent, y); // Update all words with modified characters based on the value of y
      }, 200); // Update every 1000 milliseconds
    }
  
    function modifyWords(words, y) {
  const modifiedWords = words.map((word, index) => {
    const yRanges = [0, 600, 800, 900, 950, 100, 1100, 1200, 1250]; // Define the ranges of y



    for (let i = 1; i < yRanges.length; i++) {
      if (index >= i * 40 && y > yRanges[i - 1] && y <= yRanges[i]) {
        return modifyWord(word); // Modify the words based on the specified ranges of y
      }
    }
    return word; // Retain the original words
  });

  modificationCount++;
  if (modificationCount >= 5) {
    modificationCount = 0; // Reset modification count
    return originalWords; // Revert to the original words
  }
  return modifiedWords;
}
    function modifyWord(word) {
  const randomIndexes = getRandomIndexes(word.length, Math.ceil(word.length * 0.75));
  const randomCharacters = ['!', '@', '#', '$', '%', '^', '&', '*',  '҉', '̷', 'Ψ','༒',];
  const modifiedWord = word.split('').map((char, index) => {
    if (randomIndexes.includes(index)) {
      return char;
    } else {
      return randomCharacters[Math.floor(Math.random() * randomCharacters.length)];
    }
  }).join('');
  return modifiedWord;
}

  function getRandomIndexes(wordLength, numToRetain) {
    const indexes = [];
    while (indexes.length < numToRetain) {
      const randomIndex = Math.floor(Math.random() * wordLength);
      if (!indexes.includes(randomIndex)) {
        indexes.push(randomIndex);
      }
    }
    return indexes;
  }
</script>
<svelte:window bind:scrollY={y} />
<div class="word-container">
  {#each splitContent as word}
    <span class="no-wrap">{word}&nbsp;</span>
  {/each}
</div>

<style>
    .word-container {
      white-space: pre-wrap;
    }
  
    .no-wrap {
      white-space: nowrap;
    }
  </style>