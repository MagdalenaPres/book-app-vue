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
                <th>Pages</th>
                <th>Options</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="book in allBooks" :key="book.id">
                <td>{{ book.id }}</td>
                <td>{{ book.title }}</td>
                <td>{{ book.pages }}</td>
                <td>
                  <svg xmlns="http://www.w3.org/2000/svg" 
                   width="20" height="20" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
                    <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
                    <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
                  </svg>
                  <svg xmlns="http://www.w3.org/2000/svg" @click="deleteBook(a.id)"
                   width="20" height="20" fill="currentColor" class="bi bi-trash3" viewBox="0 0 16 16">
                    <path d="M6.5 1h3a.5.5 0 0 1 .5.5v1H6v-1a.5.5 0 0 1 .5-.5ZM11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3A1.5 1.5 0 0 0 5 1.5v1H2.506a.58.58 0 0 0-.01 0H1.5a.5.5 0 0 0 0 1h.538l.853 10.66A2 2 0 0 0 4.885 16h6.23a2 2 0 0 0 1.994-1.84l.853-10.66h.538a.5.5 0 0 0 0-1h-.995a.59.59 0 0 0-.01 0H11Zm1.958 1-.846 10.58a1 1 0 0 1-.997.92h-6.23a1 1 0 0 1-.997-.92L3.042 3.5h9.916Zm-7.487 1a.5.5 0 0 1 .528.47l.5 8.5a.5.5 0 0 1-.998.06L5 5.03a.5.5 0 0 1 .47-.53Zm5.058 0a.5.5 0 0 1 .47.53l-.5 8.5a.5.5 0 1 1-.998-.06l.5-8.5a.5.5 0 0 1 .528-.47ZM8 4.5a.5.5 0 0 1 .5.5v8.5a.5.5 0 0 1-1 0V5a.5.5 0 0 1 .5-.5Z"/>
                  </svg>
                </td>
          </tr>
        </tbody>
    </table>
  </div>
  <br>
  
  <div> 
      <form class="adding">
        <input v-model="title" placeholder="Enter title">
        <input v-model="pages" placeholder="Enter pages">
        <input v-model="author" placeholder="Enter author id">
        <button type="submit" @click="addBook">Add book</button>
      </form>
    </div>
    <br>
    <div> 
      <form class="updating">
        <input v-model="newTitle" placeholder="Enter title">
        <input v-model="newPages" placeholder="Enter pages">
        <input v-model="newAuthor" placeholder="Enter author id">
        <button id="update" type="submit" @click="updateBook">Update book</button>
      </form>
  </div>  
</template>

<script>
import axios from 'axios'
import 'mdb-vue-ui-kit/css/mdb.min.css';

export default {
  data() {
    return {
      loading: false,
      bookId: 1,
      post: null,
      error: null,
      allBooks: null,
    }
  },
  mounted () {
    axios
      .get('http://localhost:8080/get/books')
      .then(response => (this.allBooks = response.data))
  },
  methods:{
    addBook() {
       axios
        .post('http://localhost:8080/create/book/', {
            title: this.title,
            pages: this.pages,
            author: this.author
          }
        )
    },
    updateBook() {
       axios
        .put('http://localhost:8080/update/book/' + this.bookId, {
            title: this.newTitle,
            pages: this.newPages,
            author: this.newAuthor
          }
        )
    },
    deleteBook(id) {
       axios
        .delete('http://localhost:8080/delete/book/' + id)
    }
  }
}
</script>

<style scoped>

    button {
      width: 150px;
      align-items: center;
      background: linear-gradient(to bottom right, #7ed276, #e8fde4);
      border: 0 solid #E2E8F0;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
      box-sizing: border-box;
      color: #1A202C;
    }

    input, button {
      height: 50px;
    }
    .adding {
      margin-left: 30%;
      max-width: 700px;
      display: flex;
      justify-content: space-between;
    }
    .updating {
      margin-left: 30%;
      max-width: 700px;
      display: flex;
      justify-content: space-between;
    }
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
    #add{
      align-items: center;
      background: linear-gradient(to bottom right, #7ed276, #e8fde4);
      border: 0 solid #E2E8F0;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
      box-sizing: border-box;
      color: #1A202C;
      display: inline-flex;
      font-family: Inter, sans-serif;
      font-size: 1rem;
      font-weight: 700;
      height: 56px;
      justify-content: center;
      padding: 24px;
      text-decoration: none;
      width: auto;
      border-radius: 8px;
      cursor: pointer;
      float: right;
      margin-right: 120px;
      margin-bottom: 20px;
    }

</style>
