<script setup>
import { ref } from 'vue'

const props = defineProps(['paramValue'])

const emit = defineEmits(['update'])
const val = ref(props.paramValue)
</script>

<template>
	<div class="">
		<p>Change the value that the URL param uses:</p>
		<form @submit.prevent="$emit('update', val)">
			<input type="text" v-model="val" class="p-2 border border-black mr-2 rounded" />
			<button type="submit" class="border border-black py-2 px-4 rounded">Change</button>
		</form>
	</div>
</template>

<style scoped>
</style>
