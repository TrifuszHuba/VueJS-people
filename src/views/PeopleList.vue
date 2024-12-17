<script setup lang="ts">
import PeopleCard from '@/components/PeopleCard.vue';
import data_people from '@/data/data_people';
import type People from '@/types/People';
import { ref } from 'vue';

const peopleList = ref<People[]>(data_people.getPeople());
const currentSortOrder = ref<'asc' | 'desc'>('asc');

const sortPeopleList = () => {
  peopleList.value.sort((a, b) => {
    const fullNameA = `${a.first_name} ${a.last_name}`.toLowerCase();
    const fullNameB = `${b.first_name} ${b.last_name}`.toLowerCase();
    if (fullNameA < fullNameB) return currentSortOrder.value === 'asc' ? -1 : 1;
    if (fullNameA > fullNameB) return currentSortOrder.value === 'asc' ? 1 : -1;
    return 0;
  });
};

const toggleSortOrder = () => {
  currentSortOrder.value = currentSortOrder.value === 'asc' ? 'desc' : 'asc';
  sortPeopleList();
};

sortPeopleList();
</script>

<template>
  <div class="container my-5">
    <div class="text-center mb-5">
      <h1 class="display-3">People</h1>
      <button @click="toggleSortOrder" class="btn btn-lg btn-outline-primary mt-3">
        Sort {{ currentSortOrder === 'asc' ? 'A-Z' : 'Z-A' }}
      </button>
    </div>
    <div class="row row-cols-1 row-cols-md-2 row-cols-lg-4 g-4">
      <div class="col d-flex align-items-stretch" v-for="person in peopleList" :key="person.id">
        <PeopleCard :person="person" class="card h-100" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  background-color: #f8f9fa;
  padding: 2rem;
  border-radius: 0.5rem;
}
h1 {
  color: #343a40;
}
button {
  margin-top: 1rem;
}
</style>