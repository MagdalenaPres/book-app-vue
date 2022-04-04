<template>
 <div id="authors-table">
    <table>
        <tbody>
            <tr v-for="author in authorsSource" :key="author.id">
                <td>{{ author.name }}</td>
                <td>{{ author.email }}</td>
                <td>{{ author.phone }}</td>
            </tr>
        </tbody>
    </table>
 </div>
</template>

<script>
  export default {
    name: 'author-table',
    props: {
      authorsSource: Array,
    },
  }
</script>
<style scoped></style>