<template>
  <div>
   
<div class="container">


<div class="row">



  <div class="col-md-7">

<table class="table">
<thead>
  <tr>
    <th scope="col">No</th>
    <th scope="col">Name</th>
    <th scope="col">Address</th>
    <th scope="col">Mobile</th>
    <th scope="col">Action</th>
  </tr>
</thead>
<tbody>


  <tr v-for="employee in result" v-bind:key="employee.id">
          
          <td>{{ employee.id }}</td>

          <td>{{ employee.name }}</td>
          <td>{{ employee.address }}</td>
          <td>{{ employee.mobile }}</td>
         
            <td>
            <button type="button" class="btn btn-warning" @click="edit(employee)">Edit</button>
            <button type="button" class="btn btn-danger"  @click="remove(employee)">Delete</button>
        
          </td>
        </tr>




</tbody>
</table>

</div>


<div class="col-md-5">



  <form @submit.prevent="save">
  <div class="form-group">
    <label>Employee name</label>
    <input type="text" v-model="employee.name" class="form-control"  placeholder="Employee name">
  
  </div>
  <div class="form-group">
    <label>Employee Address</label>
    <input type="text" v-model="employee.address" class="form-control"  placeholder="Employee Address">
  
  </div>
 
  <div class="form-group">
    <label>Mobile</label>
    <input type="text" v-model="employee.mobile" class="form-control"  placeholder="Mobile">
  
  </div>
 
  <button type="submit" class="btn btn-primary">Save</button>
</form>

</div>
</div>

</div>

  </div>
</template>

<script>
  
    import axios from 'axios';
 
 


export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

data(){
  return{

    result: {},


        employee:{
                   id: '',
                   name: '',
                   address: '',
                   mobile: ''
 
                  }
        }
      
    },


    created() {
        this.EmployeeLoad();
    },
    mounted() {
          console.log("mounted() called.......");
        
      },
 
    methods: {
           EmployeeLoad()

  

  {
                 var page = "http://127.0.0.1:8000/api/employees";
                 axios.get(page)
                  .then(
                      ({data})=>{
                        console.log(data);
                        this.result = data;
                      }
                  );
           },

          
save()
           {
            if(this.employee.id == '')
              {
                this.saveData();
              }
              else
              {
                this.updateData();
              }      
 
           },
           saveData()
           {
            axios.post("http://127.0.0.1:8000/api/save", this.employee)
            .then(


            ()=>{
                console.log("successfully added");
                this.EmployeeLoad();
              }
          
            )
 
           },
           edit(employee)
           {
            this.employee = employee;
          
           },
           updateData()
           {
              var editrecords = 'http://127.0.0.1:8000/api/update/'+ this.employee.id;
              axios.put(editrecords, this.employee)
              .then(
                ()=>{
                  this.employee.name = '';
                  this.employee.address = '',
                  this.employee.mobile = ''
                  this.id = ''
                  alert("Updated!!!");
                  this.EmployeeLoad();
                }
              );
 
           },
 
           remove(employee){
 
             var url = `http://127.0.0.1:8000/api/delete/${employee.id}`;
 
 
 
             // var url = 'http://127.0.0.1:8000/api/delete/'+ employee.id;
              axios.delete(url);
              alert("Deleteddd");
              this.EmployeeLoad();
            }
      }











}

</script>

