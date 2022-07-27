<script setup>
import { ref }  from 'vue'
import { useUsersStore } from '@/stores/users'
import Header from '@/components/Header.vue'
import { onMounted } from '@vue/runtime-core'
import { Octokit } from "https://cdn.skypack.dev/@octokit/core";
import PersonLink from '../components/PersonLink.vue'
import { storeToRefs } from 'pinia';
const {users} = storeToRefs(useUsersStore())
const topUsers = ["GrahamCampbell","fabpot","weierophinney","rkh","josh"]

onMounted(async() => {
  users.value = []
  const octokit = new Octokit({
    auth: import.meta.env.VITE_GITHUB_TOKEN
  })
  topUsers.map(async(user) => {
    const { data } = await octokit.request('GET /users/{username}', {
      username: user
    })
    users.value.push(data)
  })
  
})

</script>

<template>
  <main>
    <Header />
    
    <section class="px-12">
        <h1 class="text-2xl font-semibold mb-4">Top 5 Github Users</h1>
        <p class="mb-12">Tap the username to see more information</p>
        <ul class="grid grid-cols-2 md:grid-cols-5 gap-4">
          <li v-for="user in users" :key="user.id">
            <router-link :to="`/person/${user.login}`" >
              <PersonLink :user="user" />
            </router-link>
          </li>
        </ul>
    </section>
    
  </main>
</template>
