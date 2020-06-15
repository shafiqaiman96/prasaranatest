<template>
  <v-app id="login" class="primary">
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4 lg4>
            <v-card class="elevation-1 pa-3">
              <v-card-text>
                <div class="layout column align-center">
                  <img src="../static/rapid.png" alt="rapid_logo" width="120" height="120">
                  <h2 class="flex my-4 primary--text" style="text-align: center">Preventive Maintenance Checklist</h2>
                </div>
                <v-form>
                  <v-text-field append-icon="person" name="login" label="Username" type="text" v-model="name"></v-text-field>
                  <a class="errMsg" v-bind:class="err.name.isValid ? '' : 'invalid'">{{err.name.text}}</a>
                  <v-text-field append-icon="lock" name="password" label="Password" id="password" type="password" v-model="pwd"></v-text-field>
                  <a class="errMsg" v-bind:class="err.pwd.isValid ? '' : 'invalid'">{{err.pwd.text}}</a>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn block color="primary" v-on:click="doLogin">Login</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import {getUser} from '@/api/user';

  export default {
  name: 'Login',
  layout: 'default',
  data() {
    return {
      name: "",
      pwd: "",
      err: {
        name: {
          isValid: true,
          text: "Username is invalid"
        },
        pwd: {
          isValid: true,
          text: "Password is invalid"
        },
      }
    }
  },
   methods: {
    doLogin: function() {
      var hasErr = false;
      this.err.name.isValid = true;
      this.err.pwd.isValid = true;
      if(!this.name || this.name !== 'abc'){
        this.err.name.isValid = false;
        hasErr = true;
      }
      if(!this.pwd || this.pwd !== '123'){
        this.err.pwd.isValid = false;
        hasErr = true;
      }
      if(hasErr == true){
        alert('Authentication failed!\nPlease check your Username and Password');
      }
      if(hasErr == false){
        this.loading = true;
        this.$router.push({ path: '/'});
      }
    }
  },
  computed: {
    users() {
      return getUser();
    }
  }
}
</script>
<style scoped lang="css">
  #login {
    height: 50%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    content: "";
    z-index: 0;
  }
  .errMsg{
  color: red;
  display: none;
  }
  .errMsg.invalid{
    display: block;
  }

</style>
