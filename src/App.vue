<script setup>
import { ref } from 'vue';

import LinkList from './components/LinkList.vue'
import AddParam from './components/AddParam.vue'
import ChangeValue from './components/ChangeValue.vue'

const extraParamsFromStorage = JSON.parse(window.localStorage.getItem('extraParams') ?? '[]');
const extraParams = ref(extraParamsFromStorage);

const addExtraParams = (params) => {
  extraParams.value = [...new Set(extraParams.value.concat(params))];
  window.localStorage.setItem('extraParams', JSON.stringify(extraParams.value));
}

const removeExtraParam = (param) => {
  extraParams.value = extraParams.value.filter(p => p !== param);
  window.localStorage.setItem('extraParams', JSON.stringify(extraParams.value));
}

const paramValue = ref(window.localStorage.getItem('paramValue') ?? 'test');
const setParamValue = (val) => {
  paramValue.value = val;
  window.localStorage.setItem('paramValue', val);
}
</script>

<template>
  <div class="p-4">
    <div class="my-4">
      <h1 class="text-2xl">URL Tracker Tests</h1>
      <p>Test which URL trackers are working and which are not.</p>
      <p>Safari and Firefox are now removing some URL trackers. Chrome extensions like uBlock Origin also block some parameters.</p>
      <p>Check which work and which don't by clicking on the links on this page.</p>
      <p>If it appears <span class="text-green-500">green</span> after clicking, it works. <span class="text-red-500">Red</span>, it doesn't work.</p>
    </div>
    <div class="my-4">
      <LinkList class="my-4" :extraParams="extraParams" :paramValue="paramValue" @removeParam="removeExtraParam" />
      <div class="flex gap-8 my-4">
        <AddParam @add="addExtraParams" />
        <ChangeValue @update="setParamValue" :paramValue="paramValue" />
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
