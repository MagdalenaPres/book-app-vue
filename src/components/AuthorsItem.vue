<template>
    <div>
        <p class="authors-title"> 
            <slot name="header"></slot>
        </p>
    </div>
    <div> 
  <div class="add-authors"> 
     <form class="adding">
       <input v-model="name" placeholder="Enter Name">
       <input v-model="surname" placeholder="Enter Surname">
       <button id="add" type="submit" v-on:click="addAuthor">Add author</button>
     </form>
   </div>
   </div> 
   <br/>
  <div class="authors-table">
    <table class="table table-bordered table-stripped">
        <thead>
            <tr>
                <th>Id</th>
                <th>Name</th>
                <th>Surname</th>
                <th>Options</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="a in allAuthors" :key="a.id">
                <td>{{ a.id }}</td>
                <td>{{ a.name }}</td>
                <td>{{ a.surname }}</td>
                <td>
                  <svg xmlns="http://www.w3.org/2000/svg" v-on:click="showModal(a)"
                      width="20" height="20" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
                    <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
                    <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
                  </svg>
                  <svg xmlns="http://www.w3.org/2000/svg" v-on:click="deleteAuthor(a.id)"
                      width="20" height="20" fill="currentColor" class="bi bi-trash3" viewBox="0 0 16 16">
                    <path d="M6.5 1h3a.5.5 0 0 1 .5.5v1H6v-1a.5.5 0 0 1 .5-.5ZM11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3A1.5 1.5 0 0 0 5 1.5v1H2.506a.58.58 0 0 0-.01 0H1.5a.5.5 0 0 0 0 1h.538l.853 10.66A2 2 0 0 0 4.885 16h6.23a2 2 0 0 0 1.994-1.84l.853-10.66h.538a.5.5 0 0 0 0-1h-.995a.59.59 0 0 0-.01 0H11Zm1.958 1-.846 10.58a1 1 0 0 1-.997.92h-6.23a1 1 0 0 1-.997-.92L3.042 3.5h9.916Zm-7.487 1a.5.5 0 0 1 .528.47l.5 8.5a.5.5 0 0 1-.998.06L5 5.03a.5.5 0 0 1 .47-.53Zm5.058 0a.5.5 0 0 1 .47.53l-.5 8.5a.5.5 0 1 1-.998-.06l.5-8.5a.5.5 0 0 1 .528-.47ZM8 4.5a.5.5 0 0 1 .5.5v8.5a.5.5 0 0 1-1 0V5a.5.5 0 0 1 .5-.5Z"/>
                  </svg>
                </td>
          </tr>
        </tbody>
    </table>
  </div>
<div
    className="update-modal"
    id="modal"
    role="dialog"
    v-show="isModalVisible">
    <div className="box">
      <div className="modal-content">
        <div className="modal-header">
        <button type="button" className="close" v-on:click="closeModal">
        <span aria-hidden="true">&times;</span>
        </button>
        </div>
        <div className="modal-body">
          <form className="update-author-form">
            Id:
            <input className="input-data" v-model="this.authorId">
            Name:
            <input className="input-data" v-model="this.authorName">
            Surname:
            <input className="input-data" v-model="this.authorSurname">
            <button id="update" type="submit" v-on:click="updateAuthor">Update author</button>
        </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import 'mdb-vue-ui-kit/css/mdb.min.css';

export default {
  data() {
    return {
      isModalVisible: false,
      loading: false,
      authorId: null,
      authorName: null,
      authorSurname: null,
      post: null,
      error: null,
      allAuthors: null,
      submitting: false,
      success: false,
    }
  },
  mounted () {
    axios
      .get('http://localhost:8080/get/authors')
      .then(response => (this.allAuthors = response.data))
  },
  methods:{
    searchForAuthor(authorId) {
      axios
        .get('http://localhost:8080/get/author/'+authorId)
        .then(response => (this.allAuthors = response.data))

      this.updatedAuthor = {
        id: searchedAuthor[0].id,
        Name: searchedAuthor[0].Name,
        Surname: searchedAuthor[0].Surname,
      };
    },
    addAuthor() {
       axios
        .post('http://localhost:8080/create/author/', {
          name: this.name,
          surname: this.surname
          }
        )
    },
    updateAuthor() {
       axios
        .put('http://localhost:8080/update/author/' + this.authorId, {
            id: this.authorId,
            name: this.authorName,
            surname: this.authorSurname
          }
        )
    },
    deleteAuthor(id) {
       axios
        .delete('http://localhost:8080/delete/author/' + id)
      window.location.reload();
    },
    showModal(a) {
        this.isModalVisible = true;
  
        this.authorName = a.name
        this.authorSurname = a.surname
        this.authorId = a.id
    },
    closeModal() {
      this.isModalVisible = false;
    }
  }
}
</script>

<style scoped>

    .adding {
      margin-left: 30%;
      max-width: 700px;
      display: flex;
      justify-content: space-between;
    }
    .updating {
      margin-left: 20%;
      max-width: 900px;
      display: flex;
      justify-content: space-between;
    }
    .authors-title{
        margin-top: 80px;
        font-size: 2.2rem;
        text-align: center;
        font-weight: bold;
    }
    .authors-table{
        text-align: center;
    }

    button {
      align-items: center;
      background: linear-gradient(to bottom right, #7ed276, #e8fde4);
      border: 0 solid #E2E8F0;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
      box-sizing: border-box;
      color: #1A202C;
      margin-block: 5px;
    }
    .add{
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

    .update-modal {
      position: fixed;
	    left: 0;
	    top: 0;
	    width: 100%;
	    height: 100%;
      z-index: 10040;
      overflow: auto;
      overflow-y: auto;
	    background-color:rgba(0,0,0,0.6);
    }

    .update-modal.show{
    	visibility:visible;
    	opacity: 1;
    }

    .update-modal .box{
    	background-color:#ffffff;
      width: 200px;
      height: 200px;
    	position: absolute;
    	left: 50%;
    	top:50%;
    	transform:translate(-50%,-50%);
    	margin-left: 50px;
      border-radius: 4px;
      text-align: center;
    }
    .update-modal.show .box{
    	opacity: 1;
    	margin-left: 0;
    }
    .modal-content{
      text-align: center;
    }
    .input-data{
      width: -webkit-fill-available;
    }
  

</style>
