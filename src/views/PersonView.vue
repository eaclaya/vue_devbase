<script setup>
import Header from '@/components/Header.vue'
import { ref } from 'vue'
import { storeToRefs } from 'pinia';
import { useUsersStore } from '@/stores/users'
import { useRoute } from 'vue-router';
const route = useRoute();
const username = route.params.username
const user = ref(null)
const {users} = storeToRefs(useUsersStore())
user.value = users.value.find(user => user.login === username)

</script>

<template>
  <Header />
  <div class="flex flex-col border-b border-b-gray-300 py-4 px-4" v-if="user">
      <div class="flex">
        <img :src="user.avatar_url" alt="Avatar" class="rounded-full w-12" />
        <div class="ml-4">
          <h1 class="text-xl font-semibold">{{user.login}}</h1>
          <p class="text-gray-600">{{user.location}}</p>
        </div>
      </div>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
