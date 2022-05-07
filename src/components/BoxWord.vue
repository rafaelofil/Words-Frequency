<script setup lang="ts">
  import { computed, ref } from 'vue';

  let text = ref<string>("");
  let wordsFrequency = ref([{word: "", frequency: 0}]);

  const words = computed(() => text.value.split(/[^A-ZÀ-ź]/gi).filter((item) => item != "").sort());
  
 function countWords() {
    wordsFrequency.value = [];
    let i = 1;

    wordsFrequency.value[0] = {
      word: words.value[0],
      frequency: 1,
    };

    if(words.value.length > 0)
      howManyWordsRepeat(i)
  }

  function howManyWordsRepeat(i: number) {
      words.value.reduce((previousItem, actualItem) => {
      if (previousItem === actualItem) {
        wordsFrequency.value[i - 1].frequency++;
        return previousItem;
      } else {
        wordsFrequency.value[i] = {
        word: actualItem,
        frequency: 1,
      };
        i++;
        return actualItem;
      }
    });
  }

</script>

<template>
	<div class="container-text">
		<textarea id="text" name="text" rows="10" v-model="text" @keyup="countWords"></textarea>
		<div>
			<select name="order" id="order">
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

  border: 2px solid;
  border-collapse: collapse;
}

.container-table table,td {
  border: 2px solid var(--vt-c-black-soft);
}

.container-table td {
  width: 50%;
  text-align: center;
}

.container-table thead {
  background: var(--vt-c-black-mute);
  color: var(--vt-c-white);
  justify-content: space-around;
}

</style>