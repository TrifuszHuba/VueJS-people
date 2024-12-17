<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import type People from '@/types/People';
import data_people from '@/data/data_people';

const route = useRoute();
const router = useRouter();
const person = ref<People | null>(null);

onMounted(() => {
  const id = Number(route.params.id);
  person.value = data_people.getPeople().find(p => p.id === id) || null;
});

const goBack = () => {
  router.back();
};
</script>

<template>
  <div v-if="person" class="container my-5">
    <div class="card mx-auto" style="max-width: 600px;">
      <img :src="person.avatar" :alt="`${person.first_name} ${person.last_name}`" class="card-img-top" />
      <div class="card-body text-center">
        <h1 class="card-title">{{ person.first_name }} {{ person.last_name }}</h1>
        <p class="card-text">{{ person.email }}</p>
        <button @click="goBack" class="btn btn-primary mt-3">Vissza</button>
      </div>
    </div>
  </div>
  <div v-else class="container my-5 text-center">
    <p>Trifusz Huba</p>
    <button @click="goBack" class="btn btn-secondary mt-3">Vissza</button>
  </div>
</template>

<style scoped>
.card-img-top {
  object-fit: cover;
  height: 300px;
}
</style>