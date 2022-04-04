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
                <th>Title</th>
                <th>Author</th>
                <th>Pages</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td> </td>
                <td> </td>
                <td> </td>
            </tr>
        </tbody>
    </table>
  </div>
</template>

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
