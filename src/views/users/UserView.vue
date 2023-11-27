
<script>
import axios from "axios";

export default {
  name:"UserView",
  data(){

    return{
      users:[],
      show: null
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
    },
    formatDate(dateString) {
      const date = new Date(dateString);
      const day = date.getDate().toString().padStart(2, '0'); // Obtiene el día y asegura que tenga dos dígitos
      const month = (date.getMonth() + 1).toString().padStart(2, '0'); // Obtiene el mes (los meses comienzan desde 0)
      const year = date.getFullYear();

      return `${day}/${month}/${year}`;
    },
    toggleDetail(userId) {
      // Si el ID del usuario es igual al que ya está mostrando, ocultar el detalle
      // De lo contrario, mostrar el detalle del usuario correspondiente
      this.show = this.show === userId ? null : userId;
    }
  },
  mounted() {
    this.getUsers();
  }
}
</script>
<template>
  <!-- Acciones de la tarjeta, como botones, detallas, etc. -->
  <div class="users">
    <div class="card">
      <div class="card-header">
          <RouterLink to="/users/create" tag="v-btn">
            <v-btn>
              ADD USER
            </v-btn>
          </RouterLink>
      </div>

    <tbody v-if="users.length > 0">
    <v-row>
      <v-col
          v-for="(user, index) in users"
          :key="index"
          cols="12"
          sm="6"
          md="4"
          lg="3">
      <v-card class="mx-auto my-8 "
          max-width="344"
          elevation="16" >
        <v-card-item>
          <v-card-title>
            {{ index +1 }}. Username:  {{ user.username }}
          </v-card-title>
          <v-card-subtitle>
            Email: {{ user.email }}
          </v-card-subtitle>
        </v-card-item>

        <v-card-actions>
          <RouterLink :to="{ path: '/users/'+ user.id + '/edit' }" tag="v-btn">
            <v-btn color="teal-darken-4"
                   variant="text">
              Edit
            </v-btn>
          </RouterLink>
          <button type="button" @click="deleteUserById(user.id)" >
            <v-btn color="red-accent-4"
                   variant="text">
              Delete
            </v-btn>
          </button>
          <v-spacer></v-spacer>
          <v-btn
              color="orange-lighten-2"
              variant="text"
              @click="toggleDetail(user.id)"
          >Detail</v-btn>
        </v-card-actions>
        <v-expand-transition>
          <div v-show="show === user.id">
            <v-divider></v-divider>

            <v-card-text>
              Password: {{ user.password }}
              <v-divider></v-divider>
              First Name: {{ user.first_name }}
              <v-divider></v-divider>
              Last Name: {{ user.last_name }}
              <v-divider></v-divider>
              Age: {{ user.age }}
              <v-divider></v-divider>
              Birthday: {{ formatDate(user.birth_day) }}

            </v-card-text>
          </div>
        </v-expand-transition>
      </v-card>
      </v-col>
    </v-row>
    </tbody>

    <tbody v-else>
    <tr>
      <td colspan="7">There are no users</td>
    </tr>
    </tbody>
    </div>
  </div>
</template>

<style scoped>

</style>