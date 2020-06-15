<template>
  <!-- <v-card>
    <v-toolbar color="teal" dark>
      <v-toolbar-side-icon></v-toolbar-side-icon>
      <v-toolbar-title>Topics</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>more_vert</v-icon>
      </v-btn>
    </v-toolbar>
    <v-list>
      <v-list-group
        v-model="item.active"
        v-for="item in items"
        :key="item"
        no-action
      >
        <v-list-tile slot="activator">
          <v-list-tile-content>
            <v-list-tile-title>{{ item.content }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile v-for="subItem in item.jsonled" :key="subItem" href="#">
          <v-list-tile-content v-for="subItem2 in subItem.value" :key="subItem2">
            {{ subItem2.title }}
          </v-list-tile-content>
        </v-list-tile>
      </v-list-group>
    </v-list>
  </v-card> -->
  <v-card>
    <v-toolbar color="teal" dark>
      <v-toolbar-side-icon></v-toolbar-side-icon>
      <v-toolbar-title>Topics</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>more_vert</v-icon>
      </v-btn>
    </v-toolbar>
    <v-list two-line>
      <v-list-group>
        <v-list-tile slot="activator">
          <v-list-tile-content>
            <v-list-tile-title>contoh1</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile>
          <v-list-tile-content style="min-height: 200px;">
            <table style="padding: 30px">
                <tr>
                    <th><a>ITEM</a></th>
                    <th>CHECKLIST</th>
                    <th class="remark">REMARK</th>
                </tr>
                <tr>
                    <td>haha1</td>
                    <td>haha1</td>
                    <td>haha1</td>
                </tr>
                <tr>
                    <td>haha2</td>
                    <td>haha2</td>
                    <td>haha2</td>
                </tr>
                <tr>
                    <td>haha1</td>
                    <td>haha1</td>
                    <td>haha1</td>
                </tr>
                <tr>
                    <td>haha2</td>
                    <td>haha2</td>
                    <td>haha2</td>
                </tr>
            </table>
          </v-list-tile-content>
        </v-list-tile>
      </v-list-group>
       <v-list-group>
        <v-list-tile slot="activator">
          <v-list-tile-content>
            <v-list-tile-title>contoh1</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile>
          <v-list-tile-content style="min-height: 200px;">
            <table style="padding: 30px">
                <tr>
                    <th><a>ITEM</a></th>
                    <th>CHECKLIST</th>
                    <th class="remark">REMARK</th>
                </tr>
                <tr>
                    <td>haha1</td>
                    <td>haha1</td>
                    <td>haha1</td>
                </tr>
                <tr>
                    <td>haha2</td>
                    <td>haha2</td>
                    <td>haha2</td>
                </tr>
                <tr>
                    <td>haha1</td>
                    <td>haha1</td>
                    <td>haha1</td>
                </tr>
                <tr>
                    <td>haha2</td>
                    <td>haha2</td>
                    <td>haha2</td>
                </tr>
            </table>
          </v-list-tile-content>
        </v-list-tile>
      </v-list-group>
    </v-list>
  </v-card>
</template>

<script>
import VWidget from '@/components/VWidget';

export default {
components: {
VWidget
},
  data () {
    return {
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
                },
                {
                    title:'1.3 HARDNESS & EARTHING CHECK',
                    checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
                }
                ]
            },
            { 
                name:'BACK', 
                value : 
                [
                {
                    title:'2.1 VISUAL CHECK (FUNCTION & CLEAN)',
                    checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
                },

                {
                    title:'2.2 HARDNESS & EARTHING CHECK',
                    checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
                },
                {
                    title:'2.3 HARDNESS & EARTHING CHECK',
                    checkbox: [{label:'Weekly', cbValue:"No"}, {label:'Monthly', cbValue:"No"}, {label:'Quaterly', cbValue:"No"}, {label:'Yearly', cbValue:"No"}]
                }
                ]
            }
            ]
        }
        ]
    }
  }
};
</script>

<style scoped>
.bg-full{
  background-image: url('../static/bg/18.jpg');
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
  min-height: 720px;
}

table {
  padding-top: 20px;
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}
.remark{
  height: auto;
}
/* td {
  padding-right: 20px;
  padding-left: 20px;
  background-color: rgb(230, 254, 255);
  border: 1px solid rgb(255, 255, 255);
  border-radius: 5px;
}
th {
  padding-top: 10px;
  padding-bottom: 10px;
  padding-right: 20px;
  padding-left: 20px;
  background-color: rgb(207, 252, 253);
  border: 1px solid rgb(255, 255, 255);
  border-radius: 5px;
} */

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
