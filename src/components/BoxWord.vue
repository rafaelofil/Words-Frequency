<script setup lang="ts">
  import { computed, ref, watch } from 'vue';
  import type { Ref, ComputedRef} from 'vue';

  let text: Ref<string> = ref<string>("");
  let wordsFrequency: Ref<{word: string, frequency: number}[]> = ref([{word: "", frequency: 0}]);
  let order: Ref<string> = ref("Alphabetic Order");

  const words: ComputedRef<string[]> = computed(() => text.value.split(/[^A-ZÀ-ź]/gi).filter((item) => item != "").sort());
     
 function countWords() {
   wordsFrequency.value = [];
    let i = 1;

    if(words.value.length > 0){
      wordsFrequency.value[0] = {
        word: words.value[0],
        frequency: 1,
      };

      howManyWordsRepeat(i);
    }

    orderWords(order);
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

  function orderWords(order: string) {
    switch (order.value || order) {
      case "Alphabetic Order":
        wordsFrequency.value.sort((a, b) => (a.word > b.word ? 1 : -1));
        break;
      case "Ascending Order":
        wordsFrequency.value.sort((a, b) => a.frequency - b.frequency);
        break;
      case "Descending Order":
        wordsFrequency.value.sort((a, b) => b.frequency - a.frequency);
        break;
      default:
        wordsFrequency.value.sort((a, b) => b.frequency - a.frequency);
      }
  }
</script>

<template>
	<div class="container-text">

		<textarea id="text" name="text" rows="10" v-model="text" @keyup="countWords" placeholder="Write your text here ;)"></textarea>

    <div>
      <select name="order" id="order" v-model="order" @change="orderWords(order)">
        <option selected>Alphabetic Order</option>
        <option>Ascending Order</option>
        <option>Descending Order</option>
      </select>
    </div>

    <table class="container-table" v-if="words.length > 0">
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

  color: var(--color-heading);
  font-size: 1rem;

  background: var(--color-background);
  border: 2px solid var(--color-border);
  border-radius: 4px;
}

#text {
	border: 2px solid #000;
	border-radius: 4px;
	width: 30%;
  padding-left: 0.5rem;

  resize: none;
  outline: none;

  font-family: Inter, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu,
  Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
}

.container-table {
  width: 350px;

  border: 2px solid;
  border-collapse: collapse;
}

.container-table table,td {
  border: 2px solid var(--color-border);
}

.container-table td {
  width: 50%;
  text-align: center;

  color: var(--color-text);
}

.container-table thead {
  background: var(--color-background-mute);
  color: var(--color-heading);
  justify-content: space-around;
}

@media (max-width: 1185px) {
  #text {
    width: 350px;
  }
}

@media (max-width: 400px) {
  .container-text {
    padding: 0.5rem;
  }

  .container-text > div {
    margin: 0rem;
    width: 100%;
  }

  .container-table, #text {
    width: 100%;
  }

  #order {
    margin: 0.5rem 0;
    padding: 0rem;
  }
}

</style>