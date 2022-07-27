<script setup>
  const props = defineProps({
    user: {
      type: Object,
      required: true
    }
  })
</script>

<template>
  <button class="bg-blue-600 text-white w-40 py-2 hover:bg-blue-800">{{props.user.login}}</button>
</template>
