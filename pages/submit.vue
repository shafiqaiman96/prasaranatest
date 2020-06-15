<template>
  <div id="submit" class="bg-full">
    <v-container grid-list-xl fluid>
      <v-card>
        <v-widget :title=items[0].content class="mt-3">
          <div slot="widget-content" style="min-height: 720px; padding-left: 10px; padding-right: 10px">
            <v-card class="mx-auto" max-width="1080" style="margin: 20px; padding: 20px" min-height="300">
              <table>
                <tr>
                  <th width="30%">
                    <div v-for="(prof, index) in profile" :key="index">
                      <p style="text-align: left">{{prof}}:  </p>
                    </div>
                  </th>
                  <td width="70%" style="padding-left: 70px">
                      <div v-for="userData in this.$route.query.mainCheck[1]" :key=userData style="list-style-type:none;">
                        <p style="">
                          {{userData}} 
                        </p>
                      </div>
                  </td>
                </tr>
              </table>
              <br>
                <table style="width: 100%">
                  <tr>
                    <th style="padding-bottom: 15px">MAINTENANCE DONE</th>
                  </tr>
                  <tr>
                    <td style="text-align:left;">
                      <div v-for="keyin in this.$route.query.mainCheck[0]" :key=keyin>
                        <ol style="list-style-type:none;">
                          <li style="padding-bottom: 10px">
                            {{keyin.slice(0,-1)}} 
                            <div class="dataType" v-if="keyin.slice(-1) === '0'">
                              (Weekly)
                            </div>
                            <div class="dataType" v-else-if="keyin.slice(-1) === '1'">
                              (Monthly)
                            </div>
                            <div class="dataType" v-else-if="keyin.slice(-1) === '2'">
                              (Quarterly)
                            </div>
                            <div class="dataType" v-else-if="keyin.slice(-1) === '3'">
                              (Yearly)
                            </div>
                          </li>
                        </ol>
                      </div>
                    </td>
                  </tr>
                </table>
              </v-card>
            <v-checkbox
              label="I confirm that the information given in this form is true, complete and accurate."
              color="primary"
              class="toggle"
              true-value="Yes"
              false-value="No"
              v-model="tick"
            >
            </v-checkbox>
            <div class="button">
              <v-btn color="grey" style="text-decoration: none; color:white" to="/form">Back</v-btn>
              <v-btn style="text-decoration: none; color:white" color="green" v-on:click="alert1">Submit</v-btn>
            </div>
          </div>
        </v-widget>
      </v-card>
    </v-container>
  </div>
</template>

<script>
import VWidget from '@/components/VWidget';
import {getUser} from '@/api/user';
import VueTimepicker from 'vue2-timepicker';
import 'vue2-timepicker/dist/VueTimepicker.css'
import state from '/';
import { mapState } from 'vuex'

export default {
layout: "dashboard",
name: 'Inspect',
components: {
    VWidget,
    VueTimepicker 
  },
created() {
    // console.log(this.$route.query.mainCheck);
  },
data() {
  return {
    tick:"No",
    tab: null,
    items: [
      { tab: 'Dec', content: 'DECLARATION' }
    ],
    profile: ["Inspector Name", "Inspector ID", "Bus No.", "Bus Model", "Mainenance Order", "Date", "Time Start", "Time End"]
  };
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
  alert1() {
    if(this.tick === "Yes"){
      this.$confirm("Are you confirm to submit this form?").then(() => {
        this.$fire({
            title: "Your data already submitted",
            text: "",
            type: "success",
            timer: 3000
          })
      })
  } else {
    alert("Please confirm before submit!")
  }
       
    }
  }
};
</script>

<style scoped>
.button{
  padding-left: 85%
  }

.bg-full{
  background-color: #fafafa;
  min-height: 720px;
}
.dataType{
  color: #1976d2
}

@media screen and (max-width: 600px) {
  .button{
    padding-left: 65%
    }
}
</style>
