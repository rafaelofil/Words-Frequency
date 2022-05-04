<script setup lang="ts">


</script>

<template>
	<div class="container-text">
		<textarea id="text" name="text" rows="10"></textarea>

		<div>
			<select name="order" id="order">
        <option value="mercedes">Alphabetic Order</option>
        <option value="volvo">Ascending Order</option>
        <option value="Descending">Descending Order</option>
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
}

</style>