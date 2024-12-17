<script setup lang="ts">
import type People from '@/types/People';
import { useRouter } from 'vue-router';

const props = defineProps<{ person: People }>();
const router = useRouter();

const navigateToContact = () => {
  router.push(`/contact/${props.person.id}`);
};
</script>

<template>
  <div @click="navigateToContact" class="card h-100">
    <img :src="person.avatar" :alt="`${person.first_name} ${person.last_name}`" class="card-img-top" />
    <div class="card-body d-flex flex-column">
      <h5 class="card-title">{{ person.first_name }} {{ person.last_name }}</h5>
      <p class="card-text">{{ person.email }}</p>
    </div>
  </div>
</template>

<style scoped>
.card {
  cursor: pointer;
}
.card-img-top {
  object-fit: cover;
  height: 200px;
}
.card-body {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
</style>