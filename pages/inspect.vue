<template>
  <v-container grid-list-xl fluid class="bg-full">
    <v-card>
      <div>
        <v-tabs-items v-model="tab">
          <v-tab-item
            v-for="item in items"
            :key="item.tab"
          >
            <v-card flat>
              <v-widget :title=item.content>
                <div slot="widget-content" style="width: 300px; padding-left: 20px" v-for="(user,index) in users" :key="index">
                  <div v-if="index==0">
                    <v-alert outline :color="type" icon="check_circle" value="true" v-if="type" dismissible>
                      Welcome back {{user.name}}
                    </v-alert>
                  </div>
                </div>
              </v-widget>
              <v-layout row>
                  <v-flex xs4>
                    <v-subheader>Inspector Name</v-subheader>
                  </v-flex>
                  <div v-for="(user,index) in users" :key="index">
                    <v-flex xs8 v-if="index==0">
                      <v-text-field            
                        name="input-name"
                        color="green"
                        :value="`${user.name}`"
                        disabled
                        style="min-width: 400px;"
                      ></v-text-field>
                    </v-flex>
                  </div>
                </v-layout>
                <v-layout row>
                  <v-flex xs4>
                    <v-subheader>ID No.</v-subheader>
                  </v-flex>
                  <div v-for="(user,index) in users" :key="index">
                    <v-flex xs8 v-if="index==0">
                    <v-text-field
                      name="input-id"
                      color="black"
                      :value="`${user.id}`"
                      disabled
                      style="min-width: 400px;"
                    ></v-text-field>
                  </v-flex>
                  </div>
                </v-layout>
                  <v-layout row>
                  <v-flex xs4>
                    <v-subheader>Bus No.</v-subheader>
                  </v-flex>
                  <v-flex xs8>
                    <v-text-field
                      label="Bus No."
                      name="input-no"
                      color="black"
                    ></v-text-field>
                  </v-flex>
                </v-layout>
                <v-layout row>
                  <v-flex xs4>
                    <v-subheader>Bus Model</v-subheader>
                  </v-flex>
                  <v-flex xs8>
                    <v-text-field
                      label="Bus Model"
                      name="input-model"
                      color="black"
                    ></v-text-field>
                  </v-flex>
                </v-layout>
                <v-layout row>
                  <v-flex xs4>
                    <v-subheader>Maintenance Order</v-subheader>
                  </v-flex>
                  <v-flex xs8>
                    <v-text-field
                      label="Maintenance Order"
                      name="input-order"
                      color="black"
                    ></v-text-field>
                  </v-flex>
                      </v-layout>
                       <div style="float: right">
                        <v-btn color="green"><nuxt-link style="text-decoration: none; color:white" to="/mystepper">Form</nuxt-link></v-btn>
                        <v-btn color="light" @click="showAlert('success')">info</v-btn>
                      </div>
              </v-card>
          </v-tab-item>
        </v-tabs-items>
      </div>
    </v-card>
  </v-container>
</template>

<script>
import VWidget from '@/components/VWidget';
import {getUser} from '@/api/user';

export default {
layout: "dashboard",
name: 'Inspect',
components: {
    VWidget
  },
data() {
  return {
    tab: null,
    items: [
      { tab: 'Profile', content: 'INSPECTOR & BUS PROFILE' }
    ],
    picker: null,
    picker2: null,
    //
    arrayEvents: null,
    date1: null,
    date2: null,
    //
    date: null,
    menu: false,
    modal: false,

    type: null,
    elapse: null
  };
},
mounted() {
  this.arrayEvents = [...Array(6)].map(() => {
    const day = Math.floor(Math.random() * 30);
    const d = new Date();
    d.setDate(day);
    return d.toISOString().substr(0, 10);
  });
},
computed: {
  users() {
    return getUser();
  }
},
methods: {
  firstLetter(name) {
    return name.charAt(0);
  },
  userStatusColor(item) {
    return (item.active) ? 'green' : 'grey';
  },
  functionEvents(date) {
    const [, , day] = date.split('-');
    return parseInt(day, 10) % 3 === 0;
    },
  showAlert (type) {
      this.type = type
      
      let timer = this.showAlert.timer
      if (timer) {
        clearTimeout(timer)
      }
      this.showAlert.timer = setTimeout(() => {
          this.type = null
      }, 3000)
      
      this.elapse = 1 
      let t = this.showAlert.t
      if (t) {
        clearInterval(t)
      }
      
      this.showAlert.t = setInterval(() => {
        if (this.elapse === 3) {
          this.elapse = 0
          clearInterval(this.showAlert.t)
        }
        else {
          this.elapse++
        }
      }, 1000)
    }
  }
};
</script>

<style scoped>
.bg-full{
  background-color: #fafafa;
}

</style>
