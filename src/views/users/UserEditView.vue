
<script>
    import axios from "axios";

    export default {
      name:"UserEditView",
      data() {
        return{
          userId:'',
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
        getUserById(userId){
          axios.get(`http://localhost:8081/v1/users/${userId}`).then(res=> {
            this.model.user = res.data;
          }).catch(function (error){
            //handle error on UI Site
          })
        },
        editUser(){
          axios.put(`http://localhost:8081/v1/users/${this.userId} `,this.model.user)
              .then(res=>{
                alert('User was edited successful');

              }).catch(function (error){
            // hangle error on UI site
          })
        }
      },
      mounted() {
        this.userId=this.$route.params.id;
        this.getUserById(this.userId);
      }
    }
</script>
<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>edit user</h4>
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
          <button type="button" @click="editUser" class="btn btn-primary">
            Edit
          </button>&nbsp;&nbsp;
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