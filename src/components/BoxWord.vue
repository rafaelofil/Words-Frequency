<script setup lang="ts">
  import { ref } from 'vue';

  let text = ref("");
  let order = ref("Alphabetic Order");
  let words: Array<string> = [];
  let wordsFrequency: { word: string; frequency: number; }[] =  [];
  let i = 0;

  function splitWords() : void {
    words = text.value.toLowerCase().split(/[^A-ZÀ-ź]/gi).filter((item : string) => item != "").sort();
  }

  function countWords() : void {
    i = 1;

    wordsFrequency[0] = {
      word: words[0],
      frequency: 1,
    };

    words.reduce((previousItem, actualItem) => {
      if (previousItem === actualItem) {
        wordsFrequency[i - 1].frequency++;
        return previousItem;
      } else {
        wordsFrequency[i] = {
        word: actualItem,
        frequency: 1,
      };
        i++;
        
        return actualItem;
      }
    });
  }

  function count() : void {
    if (text.value.trim().length !== 0) {
      splitWords();
      countWords();
    }
  }
  
</script>

<template>
	<div class="container-text">
		<textarea id="text" name="text" rows="10" v-model="text" v-on:keyup="count()"></textarea>
		<div>
			<select name="order" id="order" v-model="order" v-on:click="splitWords()">
        <option>Alphabetic Order</option>
        <option>Ascending Order</option>
        <option>Descending Order</option>
      </select>
		</div>
    <table class="container-table">
      <thead>
        <th>Words</th>
        <th>Frenquency</th>
      </thead>
      <tbody>
        <tr v-for="{word, frequency} in wordsFrequency" :key="word">
          <td>{{ word }}</td>
          <td>{{ frequency }}</td>
        </tr>
      </tbody>
    </table>
	</div>
</template>

<style>
.container-text {
	width: 100%;

	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
}

.container-text > div {
	margin: 0.5rem;

	width: 350px;

	display: flex;
	justify-content: flex-start;
}

#order {
  cursor: pointer;

  width: 165px;
  padding: 0.25rem 0rem;

  color: var(--vt-c-white);
  font-size: 1rem;

  background: var(--vt-c-black-mute);
  border: 2px solid var(--vt-c-black);
  border-radius: 4px;
}

#order option {
  cursor: pointer;
}

#text {
	border: 2px solid #000;
	border-radius: 4px;
	width: 30%;

  resize: none;
}

.container-table {
  width: 350px;
}

.container-table table,td {
    border: 2px solid var(--vt-c-black-soft);
}

.container-table thead {
  background: var(--vt-c-black-mute);
  color: var(--vt-c-white);
  justify-content: space-around;
}

</style>