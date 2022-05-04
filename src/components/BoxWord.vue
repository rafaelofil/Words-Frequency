<script setup lang="ts">


</script>

<template>
	<div class="container-text">
		<textarea id="text" name="text" rows="10"></textarea>

		<div>
			<button>Order</button>
			<button>Count</button>
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

	width: 300px;

	display: flex;
	justify-content: space-between;
}

#text {
	border: 2px solid #000;
	border-radius: 4px;
	width: 300px;
}

</style>