<script setup>
    import HomeItem from "./HomeItem.vue";
</script>

<template>
  <HomeItem>
    <template #header>
        Welcome on administrator site of our library!
    </template>

    <template #notes>
        You can manage books and authors here
    </template>
  </HomeItem>
</template>
