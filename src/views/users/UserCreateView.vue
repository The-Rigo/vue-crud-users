
<script>
import axios from "axios";

export default{
  name:"UserCreateView",
  data() {
    return{
      model: {
        user:{
          username: '',
          password: '',
          email:'',
          first_name:'',
          last_name:'',
          age:'',
          birth_day:''
        }
      }
    }
  },
  methods:{
    saveUser(){
      axios.post('http://localhost:8081/v1/users',this.model.user)
          .then(res=>{
            alert('User was saved successful');
            this.model.user ={
              username: '',
              password: '',
              email:'',
              first_name:'',
              last_name:'',
              age:'',
              birth_day:''
            }
          }).catch(function (error){
            // hangle error on UI site
      })
    }
  }

}
</script>

<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>add users</h4>
      </div>
      <div class="card-body">
        <div class="mb-3">
          <label for="">Username</label>
          <input type="text" v-model="model.user.username" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Password</label>
          <input type="text" v-model="model.user.password" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Email</label>
          <input type="text" v-model="model.user.email" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">First Name</label>
          <input type="text" v-model="model.user.first_name" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Last Name</label>
          <input type="text" v-model="model.user.last_name" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Age</label>
          <input type="text" v-model="model.user.age" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Birthday</label>
          <input type="text" v-model="model.user.birth_day" class="form-control">
        </div>
        <div class="mb-3">
          <button type="button" @click="saveUser" class="btn btn-primary">
            Save
          </button>&nbsp;
          <RouterLink to="/users" class="btn btn-primary">
            Back
          </RouterLink>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>