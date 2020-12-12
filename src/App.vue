<script src="../../../../Desktop/hw__2/vue-hw_2_1/vue-hw_2_1-master/components/Guests/Guests.js"></script>
<template>
  <div id="app">
    <h2 v-if="formSubmitOk" class="success-msg">Registration completed successfully</h2>
    <h2 v-if="formSubmitNotOk" class="error-msg">Registration failed</h2>
    <Wrapper v-show="showForm" @onSubmit="onSubmit">
      <template #title>
        <h1>Registration Form</h1>
      </template>
      <template #fields>
        <Fields v-model="newUser.name" :value.sync="newUser.name" label="Name"/>
        <Fields v-model="newUser.surname" :value.sync="newUser.surname" label="Surname"/>
        <Fields v-model="newUser.email" :value.sync="newUser.email" label="Email"/>
        <div v-if="showErrorEmail" class="error-msg">Enter your email</div>
      </template>
      <template #select>
        <Select :value.sync="newUser.lang" :lang="lang"/>
      </template>
      <template #radio>
        <Radio v-model="newUser.gender" v-for="i in gender" :key="i" :label="i" :value="i"/>
      </template>
      <template #checkbox>
        <Checkbox v-model="newUser.agree" label="I`m agree" true-value="true" false-value="false"/>
        <div v-if="showErrorAgree" class="error-msg">You have to agree</div>
      </template>
      <template #submitBtn>
        <div class="submit-btn">
          <button type="submit">{{submitBtn}}</button>
        </div>
      </template>
    </Wrapper>
  </div>
</template>

<script>
import Wrapper from "./components/Wrapper";
import Select from "./components/Select";
import Fields from "./components/Fields";
import Radio from "./components/Radio";
import Checkbox from "./components/Checkbox";
export default {
  name: 'App',
  components: {
    Radio, Wrapper, Fields, Select, Checkbox
  },
  data(){
    return {
      newUser: {
        id: '',
        name: '',
        surname: '',
        email: '',
        lang: '',
        gender: '',
        agree: ''
      },
      fields: ['name', 'surname', 'email'],
      lang: ['RU', 'UA', 'EN'],
      gender: {
        male: 'male',
        female: 'female',
        other: 'other'
      },
      showForm: true,
      showErrorEmail: false,
      showErrorAgree: false,
      formSubmitOk: '',
      formSubmitNotOk: '',
      submitBtn: 'Submit form'
    }
  },
  methods:{
    onSubmit(){
      this.submitBtn = 'Sending data...'
      setTimeout(() => {
        this.showErrorAgree = false
        this.showErrorEmail = false
        this.newUser.id = Math.floor(Math.random() * Math.floor(9000000))
        if(this.newUser.email && this.newUser.agree){
          this.showForm = false
          if(this.newUser.name && this.newUser.surname){
            this.formSubmitOk = true
            this.formSubmitNotOk = false
            console.log(
              `[id]: ${this.newUser.id}
[name]: ${this.newUser.name}
[surname]: ${this.newUser.surname}
[email]: ${this.newUser.email}
[lang]: ${this.newUser.lang}
[gender]: ${this.newUser.gender}
[agree]: ${this.newUser.agree}`)
          }
          else{
            this.formSubmitOk = false
            this.formSubmitNotOk = true
          }
        }
        else {
          this.submitBtn = 'Submit form'
          if(!this.newUser.email){
            this.showErrorEmail = true
          }
          if(!this.newUser.agree){
            this.showErrorAgree = true
          }
        }
      }, 5000)
    }
  }
}
</script>

<style>
form{
  width: 50%;
  margin: auto;
  padding: 20px;
  background: aliceblue;
  border: 1px solid #ccc;
}
h1{
  text-align: center;
}
label{
  cursor: pointer;
}
.submit-btn{
  margin: 20px 0;
  text-align: center;
  cursor: pointer;
}
.error-msg{
  text-align: center;
  color: red;
}
.success-msg{
  text-align: center;
  color: green;
}
button{
  background: #673AB7;
  padding: 10px 20px;
  color: #fff;
}
</style>
