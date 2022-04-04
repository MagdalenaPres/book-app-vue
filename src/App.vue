<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "@/components/HelloWorld.vue";
</script>

<template>
  <header>
      <nav>
        <RouterLink to="/">Home&nbsp;&nbsp;&nbsp;</RouterLink>
        <RouterLink to="/about">About&nbsp;&nbsp;&nbsp;</RouterLink>
      </nav>
  </header>

  <RouterView />
</template>

<style>

nav {
  max-width: 1400px;
  margin: 0 auto;
}

header{
     display: flex;
     justify-content: space-between;
     text-indent: 2em;
     font-size: 25px;
     width: 400px;
     margin-top: 20px;
     margin-left: 540px;
 }
</style>
