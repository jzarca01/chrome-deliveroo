<template>
  <div class="container">
    <h1>Deliveroo Account Generator</h1>
    <div class="panel-body">
      <vue-form-generator :schema="schema" :model="model" :options="formOptions"></vue-form-generator>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import VueFormGenerator from "vue-form-generator";
import axios from 'axios'
import VueAxios from 'vue-axios'

const API = "http://apililo.localtunnel.me/deliveroo";

Vue.use(VueAxios, axios);
Vue.use(VueFormGenerator);

export default {
  data () {
    return {
      model: {
      },
    
      schema: {
        fields: [{
          type: "input",
          inputType: "email",
          label: "E-mail",
          model: "email",
          placeholder: "Email",
          validator: ["email", "required"]
        },
        {
          type: "input",
          inputType: "password",
          label: "Password",
          model: "password",
          min: 8,
          required: true,
          pattern: /.*\d+.*/g,
          hint: "Minimum 8 characters and 1 number",
          validator: ["string", "required", "regexp"]
        },
        {
          type: "submit",
          buttonText: "Create account",
          onSubmit: () => {this.createAccount(this.model.email, this.model.password)},
          validateBeforeSubmit: true
        }]
      },

      formOptions: {
        isNewModel: true,
        validateAfterChanged: true
      }
    }
  },
  methods: {
    createAccount(email, password) {
      console.log("this", this);
      this.$http.get(API).then((response) => {
        console.log(response)
      })
    }
  }
}
</script>

<style lang="scss">
body {
  background: #00ccbc;
}

.panel-body {
  width: 300px;
  height: auto;
}

h1 {
  font-size: 20px;
  color: white;
}

label, .hint {
  color: white;
}

fieldset {
  border: 1px solid white;
}

.error {
  border: 2px solid #990000;
}

.errors {
  color: #990000;
  font-weight: bold;
}
</style>
