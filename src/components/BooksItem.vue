<template>
    <div>
        <p class="books-title"> 
            <slot name="header"></slot>
        </p>
    </div>
  <div class="books-table">
    <table class="table table-bordered table-stripped">
        <thead>
            <tr>
                <th>Id</th>
                <th>Title</th>
                <th>Author</th>
                <th>Pages</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="book in allBooks" :key="book.id">
                <td>{{ book.id }}</td>
                <td>{{ book.title }}</td>
                <td>{{ book.pages }}</td>
          </tr>
        </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
import VueAxios from 'vue-axios'

export default {
  data() {
    return {
      loading: false,
      post: null,
      error: null,
      allBooks: null,
    }
  },
  mounted () {
    axios
      .get('http://localhost:8080/get/books')
      .then(response => (this.allBooks = response))
  },
}
</script>

<style scoped>
    .books-title{
        margin-top: 80px;
        font-size: 2.2rem;
        text-align: center;
        font-weight: bold;
    }
    .books-table{
        text-align: center;
        margin-top: 20px;
    }

</style>
