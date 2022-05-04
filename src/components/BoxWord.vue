<script setup lang="ts">
  import { reactive, ref } from 'vue';

  let text = ref("");
  let order = ref("Alphabetic Order");
  let words: Array<string> = [];
  let wordsFrequency: { name: string; number: number; }[] =  [];
  let i = 0;


  function splitWords() : void {
    words = text.value.toLowerCase().split(/[^A-ZÀ-ź]/gi).filter((item : string) => item != "").sort();
  }

  function countWords() : void {
    wordsFrequency = [];
    i = 1;

    wordsFrequency[0] = {
      name: words[0],
      number: 1,
    };

    words.reduce((previousItem, actualItem) => {
      if (previousItem === actualItem) {
        wordsFrequency[i - 1].number++;
        return previousItem;
      } else {
        wordsFrequency[i] = {
        name: actualItem,
        number: 1,
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
		<textarea id="text" name="text" rows="10" v-model="text"></textarea>
		<div>
			<select name="order" id="order" v-model="order" v-on:click="splitWords()">
        <option>Alphabetic Order</option>
        <option>Ascending Order</option>
        <option>Descending Order</option>
      </select>
		</div>
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

.container-text div {
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
	width: 350px;

  resize: none;
}

</style>