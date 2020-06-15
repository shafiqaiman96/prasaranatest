<template>
<v-container grid-list-xl fluid class="bg-full">
    <v-card>
      <v-widget :title=items[0].content class="mt-3">
        <div slot="widget-content">
         <div slot="widget-content" style="width: 300px; padding-left: 20px" v-for="(user,index) in users" :key="index">
            <div v-if="index==0">
              <v-alert outline type="success" :value="alert"  icon="check_circle" dismissible>
                 Welcome back {{user.name}}
              </v-alert>
            </div>
          </div>
          <v-card class="mx-auto"
              max-width="720" style="margin: 20px; padding: 20px" min-height="800">
              <v-layout row>
                <v-flex xs4>
                  <v-subheader>Inspector Name</v-subheader>
                </v-flex>
                <div xs8 v-for="(user,index) in users" :key="index==0">
                  <v-flex v-if="index==0">
                    <v-text-field            
                      name="input-name"
                      color="green"
                      :value="`${user.name}`"
                      disabled
                      class="nameid_box"
                    ></v-text-field>
                  </v-flex>
                </div>
              </v-layout>
              <v-layout row>
                <v-flex xs4>
                  <v-subheader>ID No.</v-subheader>
                </v-flex>
                <div xs8 v-for="(user,index) in users" :key="index">
                  <v-flex v-if="index==0">
                    <v-text-field
                      name="input-id"
                      color="black"
                      :value="`${user.id}`"
                      disabled
                      class="nameid_box"
                      :v-model="`${user.id}`"
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
                    class="nameid_box"
                    v-model="busNo"
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
                    class="nameid_box"
                    v-model="busModel"
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
                    class="nameid_box"
                    v-model="mainOrder"
                  ></v-text-field>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs4>
                  <v-subheader>Maintenance Date</v-subheader>
                </v-flex>
                <v-flex xs8>
                  <v-layout row wrap>
                  <v-flex xs11 sm5>
                    <v-dialog
                      ref="dialog"
                      persistent
                      v-model="modal"
                      lazy
                      full-width
                      width="290px"
                      :return-value.sync="date"
                    >
                      <v-text-field
                        slot="activator"
                        label="Select Date"
                        v-model="date"
                        prepend-icon="event"
                        readonly
                      ></v-text-field>
                      <v-date-picker v-model="date" scrollable>
                        <v-spacer></v-spacer>
                        <v-btn flat color="primary" @click="modal = false">Cancel</v-btn>
                        <v-btn flat color="primary" @click="$refs.dialog.save(date)">OK</v-btn>
                      </v-date-picker>
                    </v-dialog>
                  </v-flex>
                </v-layout>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs4>
                  <v-subheader>Start Time</v-subheader>
                </v-flex>
                <v-flex xs8>
                    <vue-timepicker class="nameid_box" format="hh:mm A" v-model="tStart" :minute-interval="5"></vue-timepicker>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs4>
                  <v-subheader>End Time</v-subheader>
                </v-flex>
                <v-flex xs8>
                    <vue-timepicker class="nameid_box" format="hh:mm A" v-model="tStop" :minute-interval="5"></vue-timepicker>
                </v-flex>
              </v-layout>
              <div style="float: right">
                <v-btn style="text-decoration: none; color:white" color="green" v-on:click="goForm"><v-icon color="white" small>assignment</v-icon> Form</v-btn>
              </div>
          </v-card>
        </div>
      </v-widget>
    </v-card>
  </v-container>
</template>

<script>
import VWidget from '@/components/VWidget';
import {getUser} from '@/api/user';
import VueTimepicker from 'vue2-timepicker';
import 'vue2-timepicker/dist/VueTimepicker.css'
import moment from 'moment'
import { mapState } from 'vuex'
import state from '/';

export default {
layout: "dashboard",
name: 'Dashboard',
components: {
    VWidget,
    VueTimepicker 
  },
data() {
  return {
    tStart: {
      hh: '01',
      mm: '00',
      A: 'AM'
    },
    tStop: {
      hh: '01',
      mm: '00',
      A: 'AM'
    },
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
    elapse: null,

    alert: true,
  };
},
created(){
    setTimeout(()=>{
      this.alert=false
    },5000)
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
  },
  localComputed() { 
    return ("haha")       
  },       
  ...mapState(['name', 'age', 'dob']),
  
  score () {
      return this.$store.state.name
    }
},
methods: {
  goForm() {
    var startTime = this.tStart.hh + ":" + this.tStart.mm + "" + this.tStart.A
    var stopTime = this.tStop.hh + ":" + this.tStop.mm + "" + this.tStop.A
    var details = [this.users[0].name, this.users[0].id, this.busNo, this.busModel, this.mainOrder, this.date, startTime, stopTime]
    console.log(details)
    this.$router.push({ path: '/form', query: { fullProfile: details } })
    },
  firstLetter(name) {
    return name.charAt(0);
  },
  userStatusColor(item) {
    return (item.active) ? 'green' : 'grey';
  },
  functionEvents(date) {
    const [, , day] = date.split('-');
    return parseInt(day, 10) % 3 === 0;
    }
  }
};
</script>

<style scoped>
.bg-full{
  background-color: #fafafa;
}
.nameid_box{
  max-width: 400px;
  padding-right: 20px;
}
</style>
