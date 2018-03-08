<template>
     <div class="row">
       <div class="col-md-12">
         <div class="card">

          <div>
          <table style="width:90%">
              <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Price</th>
                <th>Created At</th>
                <th>Updated At</th>
                <th>Seller Name</th>
              </tr>
              <tr v-for="row in rows.data">
                 <td>{{row._id}}</td>
                <td>{{row.name}}</td>
                <td>{{row.price}}</td>
               <td>{{row.createdAt}}</td>
               <td>{{row.updatedAt}}</td>
               <td>Karim Wael</td>
               </tr>
          </table>
          </div>
         </div>
         Please insert Name:
         <input v-model= "prodName" type= "text">
         Please insert Price:
         <input v-model= "prodPrice" type= "text">
         <button v-on:click="createP">Create</button>
         <br>
         Please insert prod_ID:
         <input v-model= "uID" type= "text">
         Please insert Name:
         <input v-model= "uName" type= "text">
         Please insert Price:
         <input v-model= "uPrice" type= "text">
         <button v-on:click="updateP">Update</button>
         <br>
         Please insert prod_ID:
         <input v-model= "pID" type= "text">
         <button v-on:click="deleteP">Delete</button>
         <br>
       </div>
     </div>
</template>
<script>
import axios from 'axios'
import PaperTable from 'components/UIComponents/PaperTable.vue'
const tableColumns = ['Id', 'Name', 'Price', 'CreatedAt', 'UpdatedAt', 'SellerName', '']
const tableData = [{
  id: 1,
  name: 'Dakota Rice',
  price: '$36.738',
  createdat: '15/2/2018',
  updatedat: '16/2/2018',
  sellername: 'Mo'
},
{
  id: 2,
  name: 'Minerva Hooper',
  price: '$36.738',
  createdat: '15/2/2018',
  updatedat: '16/2/2018',
  sellername: 'Mo'
}]
export default {
  components: {
    PaperTable
  },
  data () {
    return {
      table1: {
        title: 'Stripped Table',
        subTitle: 'Here is a subtitle for this table',
        columns: [...tableColumns],
        data: [...tableData]
      },
      table2: {
        title: 'Table on Plain Background',
        subTitle: 'Here is a subtitle for this table',
        columns: [...tableColumns],
        data: [...tableData]
      },
      row: [],
      pID: '',
      prodName: '',
      prodPrice: '',
      uID: '',
      uName: '',
      uPrice: ''
    }
  },
  created () {
    this.viewP()
  },
  methods: {
    AddToApi () {
      axios.post('http://localhost:3000/User')
    .then((response) => {
      console.log(response)
    })
    .catch((error) => {
      console.log(error)
    })
    },
    viewP () {
      axios.get('http://localhost:3000/api/product/getProducts')
      .then((response) => {
        this.rows = response.data
        console.log(this.rows)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    deleteP () {
      axios.delete('http://localhost:3000/api/product/deleteProduct/' + this.pID)
      .then((response) => {
        window.location.reload()
        console.log(this.rows)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    createP () {
      axios.post('http://localhost:3000/api/product/createProduct', {
        name: this.prodName,
        price: this.prodPrice
      })
      .then((response) => {
        window.location.reload()
        console.log(this.rows)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    updateP () {
      axios.patch('http://localhost:3000/api/product/updateProduct/' + this.uID, {
        name: this.uName,
        price: this.uPrice
      })
      .then((response) => {
        window.location.reload()
        console.log(this.rows)
      })
      .catch((error) => {
        console.log(error)
      })
    }
  }
}

</script>
<style>

</style>
