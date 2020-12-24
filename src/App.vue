<template>
  <v-app>
    <v-main>
      <v-card class="mx-auto overflow-hidden">
        <v-app-bar dark>
          <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>

          <v-toolbar-title>Company</v-toolbar-title>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" absolute temporary>
          <v-list nav dense>
            <v-list-item-group
              v-model="group"
              active-class="deep-purple--text text--accent-4"
            >
              <v-list-item>
                <v-list-item-icon>
                  <v-icon>mdi-home</v-icon>
                </v-list-item-icon>
                <v-list-item-title>Home</v-list-item-title>
              </v-list-item>

              <v-list-item>
                <v-list-item-icon>
                  <v-icon>mdi-account</v-icon>
                </v-list-item-icon>
                <v-list-item-title>Account</v-list-item-title>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-navigation-drawer>


        
        <v-card-title>
          Search for Name
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
          ></v-text-field>
        </v-card-title>
        <v-data-table
          :headers="headers"
          :items="info"
          :search="search"
        ></v-data-table>
      </v-card>
       <v-footer
      dark
      padless
      app 
      inset
    >
      <v-card
        class="flex"
        flat
        tile
      >
        <v-card-title class="teal">
          <strong class="subheading">Get connected with us!</strong>
  
          <v-spacer></v-spacer>
  
          <v-btn
            v-for="icon in icons"
            :key="icon"
            class="mx-4"
            dark
            icon
          >
            <v-icon size="24px">
              {{ icon }}
            </v-icon>
          </v-btn>
        </v-card-title>
      </v-card>
    </v-footer>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  name: "App",

  components: {},

  data() {
    return {
    icons: [
      'mdi-facebook',
      'mdi-twitter',
      'mdi-linkedin',
      'mdi-instagram',
    ],
      drawer: false,
      group: null,
      search: "",
      headers: [
        {
          text: "UserId",
          align: "start",
          value: "userId",
        },
        { text: "ID", value: "id" },
        { text: "Title", value: "title" },
        { text: "Completed", value: "completed" },
      ],
      info: [],
    };
  },
  mounted() {
    console.log("it is mounted");
    axios
      .get("https://jsonplaceholder.typicode.com/todos")
      .then((response) => (this.info = response.data));
  },
};
</script>

<style>
.theme--dark.v-app-bar.v-toolbar.v-sheet {
    background-color: #009688 !important;
    border-color: #009688 !important;
}

</style>