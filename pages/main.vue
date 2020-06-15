<template>
  <v-container grid-list-xl fluid class="bg-full">
    <v-card>
      <v-tabs
        v-model="tab"
        background-color="green"
        dark
      >
        <v-tab
          v-for="item in items"
          :key="item.tab"
        >
          {{ item.tab }}
        </v-tab>
      </v-tabs>

      <v-tabs-items v-model="tab">
        <v-tab-item
          v-for="item in items"
          :key="item.tab"
        >
        <v-card flat>
          <!-- <v-card-text>{{ item.content }}</v-card-text> -->
          <v-widget :title=item.content class="mt-3">
            <div slot="widget-content">
              <table v-for="(item2, index) in item.jsonled" :key="item2">
                <article class="message" :class="accordionClasses0">
                  <div class="message-header" @click="toggleAccordion2">
                    <b><a style="float: left">{{index+1}}</a> {{item2.name}}</b>        
                  </div>
                  <div class="message-body">
                    <div class="message-content">
                      <tr>
                        <th><a>ITEM</a></th>
                        <th>CHECKLIST</th>
                        <th class="remark">REMARK</th>
                      </tr>
                      <tr v-for="item3 in item2.value" :key="item3">
                        <td>{{item3.title}}</td>
                        <td><v-layout row wrap>
                            <v-flex xs12 sm6 md3 order-md1 order-sm v-for="(item3) in item3.checkbox" :key="item3">
                              <v-checkbox v-model=item3.cbValue
                              :label="`${item3.label}: ${item3.cbValue}`"
                              color="green"
                              class="toggle"
                              true-value="Yes"
                              false-value="No"
                              ></v-checkbox>
                            </v-flex>
                            </v-layout></td>
                        <td>
                          <v-layout row>
                            <v-text-field
                              multi-line
                            ></v-text-field>
                          </v-layout>
                        </td>
                      </tr>
                    </div>
                  </div>
                </article>
              </table>
            </div>
          </v-widget>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </v-card>
</v-container>
</template>
<script src="https://unpkg.com/vue"></script>
<script>
import VWidget from '@/components/VWidget';

export default {
components: {
VWidget
},
data() {
  return {
    isOpen: true,
    includeFiles: false,
    enabled: false,
    tab: null,
    menu: {menutab: 'Profile', menucont: 'INSPECTOR & BUS PROFILE' },
    items: [
      { tab: 'LBC', content: 'LED BOARD CHECKLIST',
      jsonled: [
      { 
        name:'FRONT', 
        value : 
        [
          {
            title:'1.1 VISUAL CHECK (FUNCTION & CLEAN)',
            checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
          },

          {
            title:'1.2 HARDNESS & EARTHING CHECK',
            checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
          }
        ]
      },
      // { 
      //   name:'SIDE', 
      //   value : 
      //   [
      //     {
      //       title:'2.1 VISUAL CHECK (FUNCTION & CLEAN)',
      //       checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
      //     },

      //     {
      //       title:'2.2 HARDNESS & EARTHING CHECK',
      //       checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
      //     }
      //   ]
      // },
      // { 
      //   name:'REAR', 
      //   value : 
      //   [
      //     {
      //       title:'3.1 VISUAL CHECK (FUNCTION & CLEAN)',
      //       checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
      //     },

      //     {
      //       title:'3.2 HARDNESS & EARTHING CHECK',
      //       checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
      //     }
      //   ]
      // },
      // { 
      //   name:'CONTROLLER', 
      //   value : 
      //   [
      //     {
      //       title:'4.1 CONTENT CHECK (ROUTE)',
      //       checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
      //     },

      //     {
      //       title:'4.2 VISUAL CHECK (FUNCTION & CLEAN)',
      //       checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
      //     }
      //   ]
      // },
    ] },
      { tab: 'FLS', content: 'FLEET TRACKING SYSTEM CHECK LIST' },
      { tab: 'PIS', content: 'PASSENGER INFORMATION SYSTEM' },
      { tab: 'CCTV', content: 'CCTV SYS' },
      { tab: 'FCS', content: 'FCS' },
    ],
  };
},
methods: {
        toggleAccordion0: function() {
          this.isOpen = !this.isOpen;
        },
        toggleAccordion1: function() {
          this.isOpen = !this.isOpen;
        },
        toggleAccordion2: function() {
          this.isOpen = !this.isOpen;
        }
      },
computed: {
  accordionClasses0: function() {
          return {
            'is-closed': !this.isOpen,
            'is-primary': this.isOpen,
            'is-dark': !this.isOpen
          }
  },
    accordionClasses1: function() {
          return {
            'is-closed': !this.isOpen,
            'is-primary': this.isOpen,
            'is-dark': !this.isOpen
          }
  },
      accordionClasses2: function() {
          return {
            'is-closed': !this.isOpen,
            'is-primary': this.isOpen,
            'is-dark': !this.isOpen
          }
  }
}
};
</script>

<style scoped>
.message {
      margin-left: auto;
      margin-right: auto;
    }
.message-header {
  cursor: pointer;
  padding: 15px;
  font-size: 1rem;
  text-align: center;
  background-color: rgb(207, 252, 253);
  border-radius: 5px;
}
.message-body   {
  padding: 0;
  overflow: hidden;
  transition: 0.3s ease all;
  background-color: rgb(230, 254, 255);
}
.is-closed .message-body {
  max-height: 0;
}
.message-content {
  padding: 20px;
}
.bg-full{
  background-image: url('../static/bg/18.jpg');
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
  min-height: 720px;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}
/* .remark{
  width: 300px;
} */
td {
  padding-right: 20px;
  padding-left: 20px;
  /* background-color: rgb(230, 254, 255); */
  /* border: 1px solid rgb(255, 255, 255); */
  border-radius: 5px;
}
th {
  padding-top: 10px;
  padding-bottom: 10px;
  padding-right: 20px;
  padding-left: 20px;
  /* background-color: rgb(207, 252, 253); */
  /* border: 1px solid rgb(255, 255, 255); */
  border-radius: 5px;
}

@media only screen and (min-width: 600px) {
  .remark{
    width: 25%;
  }
}

@media only screen and (min-width: 768px) {
  .remark{
      width: 25%;
    }
}

</style>
