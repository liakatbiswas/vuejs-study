<script setup>
import {ref,computed} from "vue";

let password = ref('');

const passwordStrength = computed(()=>{
let strength = (password.value.length*100)/10

  return Math.min(strength,100)
});

let firstName = ref("");
let lastName = ref("");

const fullName = computed(()=>{
  let fullName = firstName.value +" "+ lastName.value;

  return fullName;
})

</script>

<template>
<div>
  <h>{{fullName}}</h>
  <br>

  <input type="text" v-model="firstName" placeholder="Enter Your First Name">
  <br>
  <input type="text" v-model="lastName" placeholder="Enter Your Last Name">
</div>

  
  <hr>
  <div>
    <input type="password" v-model="password" placeholder="Enter your password">
  {{passwordStrength}}


  </div>
</template>

<style scoped>
</style>
