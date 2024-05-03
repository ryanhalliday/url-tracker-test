<script setup>
import { ref, computed } from 'vue'
import defaultParamList from '../assets/defaultParamList.js';

const props = defineProps({
  extraParams: {
	type: Array,
	default: []
  },
  paramValue: {
	type: String,
	default: 'test'
  }
});

defineEmits(['removeParam'])

const paramList = computed(() => {
	return defaultParamList.concat(props.extraParams);
})

const onClick = (param) => {
	window.sessionStorage.setItem('lastClick', param);
}

const url = new URL(window.location.href);
const urlParams = new Map(url.searchParams.entries());

const lastClick = window.sessionStorage.getItem('lastClick');
</script>

<template>
	<div class="flex flex-wrap gap-2">
		<div v-for="param in paramList" :key="param"
			
			class="border-2 border-black rounded-md cursor-pointer relative p-1"
			:class="{
				'bg-green-500': urlParams.has(param),
				'bg-red-500': urlParams.get('expected') == param && !urlParams.has(param),
			}"
			@click="onClick(param)">
				<a :href="`?expected=${param}&${param}=${props.paramValue}`" class="p-1 inline-block">
					{{ param }}
				</a>
				<button v-if="props.extraParams.includes(param)"
					@click.prevent="$emit('removeParam', param)"
					class="text-gray-400 p-1 inline-block">
						x
				</button>
		</div>
	</div>
</template>

<style scoped>
</style>
