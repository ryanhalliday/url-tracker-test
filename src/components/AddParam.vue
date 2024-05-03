<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add'])

const addStr = ref('')

const emitAdd = () => {
	emit('add', addStr.value.split(',').map(str => str.trim()))
	addStr.value = ''
}
</script>

<template>
	<div class="">
		<p>Add your own parameters, one at a time or comma seperated:</p>
		<form @submit.prevent="emitAdd">
			<input type="text" v-model="addStr" class="p-2 border border-black mr-2 rounded" />
			<button type="submit" class="border border-black py-2 px-4 rounded">Add</button>
		</form>
	</div>
</template>

<style scoped>
</style>
