
<script>
import axios from "axios";

export default {
  name:"UserView",
  data(){
    return{
      users:[]
    }
  },
  methods:{
    getUsers(){
      axios.get('http://localhost:8081/v1/users?detailed=1').then(res=> {
        this.users = res.data;
      })
    },

    deleteUserById(userId){
      if(confirm("Are you sure, you want to delete this data?")){
          axios.delete(`http://localhost:8081/v1/users/${userId}`).then(res=> {
            this.getUsers();
          }).catch(function (error){
            // handle error on UI site
          })
      }
    }
  },
  mounted() {
    this.getUsers();
  }
}
</script>
<template>
    <div class="users">
      <div class="card">
        <div class="card-header">
          <h4>
            Users
            <RouterLink to="/users/create" class="btn btn-primary float-end">
              Add User
            </RouterLink>
          </h4>
        </div>
        <div class="card-body">
          <table class="table table-bordered">
            <thead>
              <tr>
                <th>Nro.</th>
                <th>Username</th>
                <th>Password</th>
                <th>Email</th>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Age</th>
                <th>Birthday</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody v-if="users.length > 0">
              <tr v-for="(user, index) in this.users" :key="index">
                <td>{{ index + 1}}</td>
                <td>{{ user.username }}</td>
                <td>{{ user.password }}</td>
                <td>{{ user.email }}</td>
                <td>{{ user.first_name }}</td>
                <td>{{ user.last_name }}</td>
                <td>{{ user.age }}</td>
                <td>{{ user.birth_day.toString().replace(",","/").replace(",","/") }}</td>
                <td>
                  <RouterLink :to="{ path: '/users/'+ user.id + '/edit' }" class="btn btn-success">
                    Edit
                  </RouterLink>
                  <button type="button" @click="deleteUserById(user.id)" class="btn btn-danger" >
                    Delete
                  </button>
                </td>
              </tr>
            </tbody>
            <tbody v-else>
              <tr>
                <td colspan="7">There are no users</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
</template>

<style scoped>

</style>