<template>
 <div id="app" class="small-container">
 <h1>Autorzy</h1>
  <authors-table />
 </div>
 <author-table :authorsSource="authors"/>
</template>

<script>
 import Authors from "../components/Authors.vue"
 export default {
  name: 'app',
  components: {
    Authors,
  },
  data() {
    return {
      authors: [
        {
          id: 1,
          name: 'Adam Słodowy',
          email: 'adam.slodowy@zrobtosam.pl',
          phone: '+48 787 774 664'
        },
        {
          id: 2,
          name: 'Michał Studencki',
          email: 'ms@student.pwr.edu.pl',
          phone: '+48 600 565 454'
        },
        {
          id: 3,
          name: 'Kamila Napokaz',
          email: 'kami2003@h2.pl',
          phone: '+48 609 554 987'
        },
      ] 
    }
  },
 }
</script>

<style>
 button {
 background: #009435;
 border: 1px solid #009435;
 }
 .small-container {
 max-width: 1200px;
 }
</style>
