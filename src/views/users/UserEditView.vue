
<script>
    import axios from "axios";

    export default {
      name:"UserEditView",
      data() {
        return{
          userId:'',
          visible: false,
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

  <!-- Acciones de la tarjeta, como botones, detallas, etc. -->
  <div>

    <v-card
        class="mx-auto pa-12 pb-8"
        elevation="8"
        max-width="448"
        rounded="lg"
    >
      <v-card-item class="d-flex justify-center mb-6"><h4>EDIT USER</h4></v-card-item>
      <v-text-field
          density="compact"
          placeholder="Register username"
          variant="outlined"
          v-model="model.user.username"
          label="Username"
      ></v-text-field>
      <v-text-field
          :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
          :type="visible ? 'text' : 'password'"
          density="compact"
          placeholder="Register password"
          label="Password"
          variant="outlined"
          v-model="model.user.password"
          @click:append-inner="visible = !visible"
      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Register email"
          variant="outlined"
          v-model="model.user.email"
          label="Email"
      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Register first name"
          variant="outlined"
          v-model="model.user.first_name"
          label="First Name"
      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Register last name"
          variant="outlined"
          v-model="model.user.last_name"
          label="Last Name"
      ></v-text-field>
      <v-text-field
          density="compact"
          placeholder="Register Age"
          variant="outlined"
          v-model="model.user.age"
          label="Age"
      ></v-text-field>

      <v-text-field
          density="compact"
          placeholder="Register birthday"
          variant="outlined"
          v-model="model.user.birth_day"
          type="date"
          label="Birthday"
          class="mt-3"
      ></v-text-field>

      <v-btn
          block
          class="mb-1"
          color="teal-darken-1"
          size="large"
          @click="editUser"
      >
        Save
      </v-btn>
      <RouterLink to="/users" tag="v-btn">
        <v-btn
            block
            class="mb-1"
            color="indigo-darken-1"
            size="large"
        >
          Back
        </v-btn>
      </RouterLink>
    </v-card>
  </div>
</template>

<style scoped>

</style>