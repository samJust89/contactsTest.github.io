<template>
  <v-app style="background-color:#00ACC1;padding: 0;margin: 0;">
    <v-toolbar
    color="#00ACC1"
    style="margin-top: 4%;bottom: 2%;"
    height="10%"
    >
<v-spacer></v-spacer>
    <v-img 
   :src="require('../img/contactLogo.png')" ></v-img>
   <v-spacer></v-spacer>
  </v-toolbar>
    <div style="margin-left: 5%;margin-right: 5%;margin-top: 0%;">
  <v-table  class="elevation-2" style="border-radius: 10px;">
    <thead> 
      <tr>
        <th class="text-center">
         Name
        </th>
        <th class="text-center">
         Contact Number
        </th>
        <th class="text-center">
         Contact Details
        </th>
      </tr>
    </thead>
    <tbody>
      <tr class="text-center"
      v-for="item in Users"
        :key="item.id"
      >
      <td>
        <v-chip color="#00ACC1">
          {{ item.firstname + " "+ item.lastname }}
      </v-chip>
        </td>
        <td>
          <v-chip color="#00ACC1">
            {{ item.contactnumber }}
      </v-chip>
        </td>
        <td>
          <v-btn icon="mdi-account" size="x-small" color="#00ACC1" @click="viewDetails(item)"></v-btn>
        </td>
    </tr>
    </tbody>
  </v-table>
  </div>
</v-app>

<v-dialog
      v-model="dialog"
      width="30%"
    >
      <v-card color="#00ACC1">
        <br>
        <v-img style="align-self: center;"
   :src=imageProfile width="40%"></v-img>
   <v-card-text style="align-self: left;">
            <span>First Name: {{fName }}</span>
          </v-card-text>
          <v-card-text style="align-self: left;">
            <span>Last Name: {{lName }}</span>
          </v-card-text>
          <v-card-text style="align-self: left;">
            <span>Contact Number: {{contact }}</span>
          </v-card-text>
          <v-card-text style="align-self: left;">
            <span>Email: {{email }}</span>
          </v-card-text>
          <br><br>
        <v-card-actions>
          <v-btn color="white" block @click="dialog = false"   variant="outlined">Close Dialog</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>
<script>
  import axios from 'axios'

export default{
data(){
  return{
    Users:{},
    dialog: false,
    fName: "",
    lName: "",
    contact:"",
    email:"",
    imageProfile:""
    
  }
},
  methods:{
    getPost(){
      axios.get('https://my-json-server.typicode.com/samJust89/Contacts/Users').then((response)=>{
          this.Users=response.data;
      }).catch((error)=>{
        console.log(error);
      });
    },
    viewDetails(item){
      console.log(item);
      this.dialog=true;
      this.fName=item.firstname;
      this.lName=item.lastname;
      this.contact=item.contactnumber;
      this.email=item.email;
      this.imageProfile=item.pic

    }
  },
  beforeMount() {
   this.getPost();
},
}
</script>
<style>
.title{
font-size: 150%;
color:#FFFFFF;
}
</style>