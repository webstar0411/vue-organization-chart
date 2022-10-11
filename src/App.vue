/**
 *  CREATED AT 2022.10.12
 *  CREATED BY webstar0411@gmail.com
 */


<template>
  <section class="main-content">
    <chart :data="userData" @onUpdate="handleUpdate"></chart>
  </section>
</template>

<script setup>
import { ref } from "vue";
import Chart from "./components/chart/index.vue";
import sampleData from "./sample.json";

const userData = ref(sampleData);

function handleUpdate(newNode) {
  // changes one record of userdata that matches with newNode's id
  const newUserData = userData.value.map((item) => {
    if (item.id === newNode.id) return newNode;
    return item;
  });

  userData.value = newUserData;
}
</script>
