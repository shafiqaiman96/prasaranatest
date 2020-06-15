<template>
  <div id="page-steppers" class="bg-full">
    <v-container grid-list-xl fluid>
      <v-layout row wrap>
        <v-flex sm12>
          <v-stepper v-model="step">
            <v-stepper-header class="stepheader" style="background-color: #a0c3ef; width: 100%!important">
              <div v-for="(item, index) in items" :key="index">
                  <v-stepper-step :step="index+1" :complete="step > (index+1)">{{item.content}}</v-stepper-step>
                  <v-divider></v-divider>
              </div>
            </v-stepper-header>
            <v-stepper-items v-for="(item, index) in items" :key="index">
              <v-stepper-content step=1 v-if="index==0">
                <v-card class="mb-5" height="100%">
                  <v-tabs-items v-model="tab">
                    <v-card>
                      <v-widget :title="`${item.content}`" class="mt-3">
                        <div slot="widget-content">
                          <table>
                            <div v-for="(item2, index) in item.jsonled" :key="item2">
                              <div class="message-header"  >
                                  <b><a style="float: left; color: black">{{index+1}}</a> {{item2.name}}</b>        
                              </div>
                              <div class="message-body">
                                <div class="message-content">
                                  <thead>
                                    <tr>
                                      <th>ITEM</th>
                                      <th>CHECKLIST</th>
                                      <th>REMARK</th>
                                    </tr>
                                   </thead>
                                    <tr v-for="(item3,i) in item2.value" :key="i" style="padding-bottom: 10px">
                                      <td>{{item3.title}}</td>
                                      <td class="chk">
                                        <v-layout row wrap>
                                          <v-flex v-for="(item4,i) in item3.checkbox" :key="i" style="padding:5px">
                                            <v-checkbox v-model="checkedValue"
                                            :label="`${item4.label}`"
                                            color="green"
                                            class="toggle"
                                            true-value="Yes"
                                            false-value="No"
                                            :value="`${item3.title}${i}`"
                                            :id="item4.label"
                                            ></v-checkbox>
                                          </v-flex>
                                        </v-layout>
                                      </td>
                                      <td class="rmk">
                                        <v-layout row>
                                          <v-text-field
                                          multi-line
                                          ></v-text-field>
                                        </v-layout>
                                      </td>
                                    </tr>
                                  </div>
                              </div>
                            </div>
                          </table>
                        </div>
                      </v-widget>
                    </v-card>
                  </v-tabs-items>
                </v-card>
                <div style="float: right">
                  <v-btn color="grey" style="text-decoration: none; color:white" v-on:click="alert1">Cancel</v-btn>
                  <v-btn style="text-decoration: none; color:white" color="green" @click.native="step = 2">Continue</v-btn>
                </div>
              </v-stepper-content>
              <v-stepper-content step="2" v-if="index==1">
                <v-card class="mb-5" height="100%">
                  <v-tabs-items v-model="tab">
                    <v-card>
                      <v-widget :title="`${item.content}`" class="mt-3">
                        <div slot="widget-content">
                          <table>
                            <div v-for="(item2, index) in item.jsonled" :key="item2">
                              <div class="message-header"  >
                                  <b><a style="float: left; color: black">{{index+5}}</a> {{item2.name}}</b>        
                              </div>
                              <div class="message-body">
                                <div class="message-content">
                                  <thead>
                                    <tr>
                                      <th>ITEM</th>
                                      <th>CHECKLIST</th>
                                      <th>REMARK</th>
                                    </tr>
                                   </thead>
                                    <tr v-for="(item3,i) in item2.value" :key="i" style="padding-bottom: 10px">
                                      <td>{{item3.title}}</td>
                                      <td class="chk">
                                        <v-layout row wrap>
                                          <v-flex v-for="(item4,i) in item3.checkbox" :key="i" style="padding:5px">
                                            <v-checkbox v-model="checkedValue"
                                            :label="`${item4.label}`"
                                            color="green"
                                            class="toggle"
                                            true-value="Yes"
                                            false-value="No"
                                            :value="`${item3.title}${i}`"
                                            :id="item4.label"
                                            ></v-checkbox>
                                          </v-flex>
                                        </v-layout>
                                      </td>
                                      <td class="rmk">
                                        <v-layout row>
                                          <v-text-field
                                          multi-line
                                          ></v-text-field>
                                        </v-layout>
                                      </td>
                                    </tr>
                                  </div>
                              </div>
                            </div>
                          </table>
                        </div>
                      </v-widget>
                    </v-card>
                  </v-tabs-items>
                </v-card>
              <div style="float: right">
                <v-btn color="grey" style="text-decoration: none; color:white" @click.native="step = 1">Back</v-btn>
                <v-btn style="text-decoration: none; color:white" color="green" @click.native="step = 3">Continue</v-btn>
              </div>
              </v-stepper-content>
              <v-stepper-content step="3" v-if="index==2">
                <v-card class="mb-5" height="100%">
                  <v-tabs-items v-model="tab">
                    <v-card>
                      <v-widget :title="`${item.content}`" class="mt-3">
                        <div slot="widget-content">
                          <table>
                            <div v-for="(item2, index) in item.jsonled" :key="item2">
                              <div class="message-header"  >
                                  <b><a style="float: left; color: black">{{index+7}}</a> {{item2.name}}</b>        
                              </div>
                              <div class="message-body">
                                <div class="message-content">
                                  <thead>
                                    <tr>
                                      <th>ITEM</th>
                                      <th>CHECKLIST</th>
                                      <th>REMARK</th>
                                    </tr>
                                   </thead>
                                    <tr v-for="(item3,i) in item2.value" :key="i" style="padding-bottom: 10px">
                                      <td>{{item3.title}}</td>
                                      <td class="chk">
                                        <v-layout row wrap>
                                          <v-flex v-for="(item4,i) in item3.checkbox" :key="i" style="padding:5px">
                                            <v-checkbox v-model="checkedValue"
                                            :label="`${item4.label}`"
                                            color="green"
                                            class="toggle"
                                            true-value="Yes"
                                            false-value="No"
                                            :value="`${item3.title}${i}`"
                                            :id="item4.label"
                                            ></v-checkbox>
                                          </v-flex>
                                        </v-layout>
                                      </td>
                                      <td class="rmk">
                                        <v-layout row>
                                          <v-text-field
                                          multi-line
                                          ></v-text-field>
                                        </v-layout>
                                      </td>
                                    </tr>
                                  </div>
                              </div>
                            </div>
                          </table>
                        </div>
                      </v-widget>
                    </v-card>
                  </v-tabs-items>
                </v-card>
              <div style="float: right">
                <v-btn color="grey" style="text-decoration: none; color:white" @click.native="step = 2">Back</v-btn>
                <v-btn style="text-decoration: none; color:white" color="green" @click.native="step = 4">Continue</v-btn>
              </div>
              </v-stepper-content>
              <v-stepper-content step="4" v-if="index==3">
                <v-card class="mb-5" height="100%">
                  <v-tabs-items v-model="tab">
                    <v-card>
                      <v-widget :title="`${item.content}`" class="mt-3">
                        <div slot="widget-content">
                          <table>
                            <div v-for="(item2, index) in item.jsonled" :key="item2">
                              <div class="message-header"  >
                                  <b><a style="float: left; color: black">{{index+1}}</a> {{item2.name}}</b>        
                              </div>
                              <div class="message-body">
                                <div class="message-content">
                                  <thead>
                                    <tr>
                                      <th>ITEM</th>
                                      <th>CHECKLIST</th>
                                      <th>REMARK</th>
                                    </tr>
                                   </thead>
                                    <tr v-for="(item3,i) in item2.value" :key="i" style="padding-bottom: 10px">
                                      <td>{{item3.title}}</td>
                                      <td class="chk">
                                        <v-layout row wrap>
                                          <v-flex v-for="(item4,i) in item3.checkbox" :key="i" style="padding:5px">
                                            <v-checkbox v-model="checkedValue"
                                            :label="`${item4.label}`"
                                            color="green"
                                            class="toggle"
                                            true-value="Yes"
                                            false-value="No"
                                            :value="`${item3.title}${i}`"
                                            :id="item4.label"
                                            ></v-checkbox>
                                          </v-flex>
                                        </v-layout>
                                      </td>
                                      <td class="rmk">
                                        <v-layout row>
                                          <v-text-field
                                          multi-line
                                          ></v-text-field>
                                        </v-layout>
                                      </td>
                                    </tr>
                                  </div>
                              </div>
                            </div>
                          </table>
                        </div>
                      </v-widget>
                    </v-card>
                  </v-tabs-items>
                </v-card>
                <div style="float: right">
                  <v-btn color="grey" style="text-decoration: none; color:white" @click.native="step = 4">Back</v-btn>
                  <v-btn style="text-decoration: none; color:white" color="green" v-on:click="alert2">Finish</v-btn>
                </div>
              </v-stepper-content>
            </v-stepper-items>
          </v-stepper>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
  import VWidget from '@/components/VWidget';
  import dataJson from '../static/data.json'
  import Vue from "vue";
  import VueSimpleAlert from "vue-simple-alert";
 
  Vue.use(VueSimpleAlert);

  export default {
    layout: "dashboard",
    components: {
      VWidget
    },
    created() {
    // console.log(this.$route.query);
    console.log(this.$route.query.fullProfile);
    },
    data() {
      return {
        checkedValue : [],
        step: 1,
        e13: 1,
        isOpen: true,
        includeFiles: false,
        enabled: false,
        tab: null,
        menu: {menutab: 'Profile', menucont: 'INSPECTOR & BUS PROFILE' },
        items: dataJson
  };
},
    computed: {},
    methods: {
      
    alert1() {
        this.$confirm("Are you sure to cancel filling?").then(() => {
          this.$router.push({ path: '/' })
        })
    },
     alert2() {
        var profull = this.$route.query.fullProfile;
        this.$confirm("Are you sure to finish filling?").then(() => {
        this.$router.push({ path: '/submit', query: { mainCheck: [this.checkedValue, profull] } })
        console.log(profull + "----\n" + this.checkedValue)
        })
    }
    }
  };
</script>

<style scoped>

.bg-full{
  background-color: #fafafa;
}

.message {
  margin-left: auto;
  margin-right: auto;
}

.message-header {
  padding: 15px;
  font-size: 1rem;
  text-align: center;
  background-color: rgb(249, 249, 249);
  border-radius: 5px;
}

.message-body   {
  padding: 0;
  overflow: hidden;
  transition: 0.3s ease all;
  background-color: rgb(255, 255, 255);
}

.is-closed .message-body {
  max-height: 0;
}

.message-content {
  padding: 20px;
}

.rmk {
  padding-left: 50px;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100% !important;
  border: 1px solid #ccc;
  border-collapse: collapse;
  margin: 0;
  padding: 0;
  table-layout: fixed;
}

table caption {
  font-size: 1.5em;
  margin: .5em 0 .75em;
}

table tr {
  padding: .35em;
}

table td {
  padding: .625em;
  text-align: center;
  width: 1920px;
  text-align: left;
}

table th {
  font-size: 1rem;
  letter-spacing: .1em;
  text-transform: uppercase;
  width: 1920px;
}

@media screen and (max-width: 600px) {

.message-header {
  padding: 5px;
}

.message-content {
  padding: 0px;
}
  
.rmk {
  padding: 8px;
}
.chk {
  padding: 0!important;
  font-size: 0.3em;
}
  table {
    border: 0;
  }

  table caption {
    font-size: 1.3em;
  }
  
  table thead {
    border: none;
    clip: rect(0 0 0 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
  }
  
  table tr {
    border-bottom: 3px solid #ddd;
    display: block;
    margin-bottom: .625em;
    width: 100%!important;
  }
  
  table td {
    border-bottom: 1px solid #ddd;
    display: block;
    font-size: .8em;
    width: 100%!important;
    text-align: center;
  }
  
  table td::before {
    content: attr(data-label);
    float: left;
    font-weight: bold;
    text-transform: uppercase;
  }
  
  table td:last-child {
    border-bottom: 0;
  }
}

</style>

