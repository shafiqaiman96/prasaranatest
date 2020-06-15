<template>
  <v-container grid-list-xl fluid class="bg-full">
    <v-card>
      <div>
        <v-tabs-items v-model="tab">
          <v-tab-item
            v-for="item in items"
            :key="item.tab"
          >
            <v-card flat style="min-height:720px">
              <v-card-text>{{ item.content }}</v-card-text>
              <hr style="color: rgb(249, 249, 249)">
              <br>
              <div style="padding-left:20px">
                    <v-checkbox
                        label="I confirm that the information given in this form is true, complete and accurate."
                        color="green"
                        class="toggle"
                        true-value="Yes"
                        false-value="No"
                        >
                    </v-checkbox>
                </div>
            <br>
            <div style="float: right; padding-right: 30px">
                <v-btn color="grey" ><nuxt-link style="text-decoration: none; color:white" to="/mystepper">Back</nuxt-link></v-btn>
                <v-btn style="text-decoration: none; color:white" color="green" v-on:click="alert1">Submit</v-btn>
            </div>
            </v-card>
          </v-tab-item>
        </v-tabs-items>
      </div>
    </v-card>
  </v-container>
</template>

<script>
import {getUser} from '@/api/user';
export default {
layout: "dashboard",
name: 'Inspect',
data() {
  return {
    tab: null,
    items: [
      { tab: 'Profile', content: 'DECLARATION' }
    ]
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
        this.$confirm("Your data already").then(() => {
        this.$fire({
            title: "Your data already submitted",
            text: "",
            type: "success",
            timer: 3000
          })
        })
    }
  }
};
</script>

<style scoped>
.bg-full{
  background-color: #fafafa;
}

</style>
