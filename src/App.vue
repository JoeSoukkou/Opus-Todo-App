<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6">
          Opus
          </v-list-item-title>
          <v-list-item-subtitle>
            Be Productive.
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon color="grey darken-2">{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      dark
      src="1_dP81IJq-tGFxy1rIK3RYsg.png"
      scroll-target="#scrolling-techniques-2"
      
    
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          
        ></v-img>
      </template>

      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-app-bar-title>Opus - Be Productive</v-app-bar-title>

      <v-spacer></v-spacer>

  

    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
     <v-footer padless>
    <v-col
      class="text-center"
      cols="12"
    >
      © {{ new Date().getFullYear() }} Built by Y. Soukkou — <strong>Opus</strong>
    </v-col>
  </v-footer>
  </v-app>
  
</template>

<script>
  export default {
    data: () => ({
       drawer: null, 
        items: [
          { title: 'Tasks', icon: 'mdi-format-list-checks', to: "/"},
          { title: 'About', icon: 'mdi-information', to: "/about"},
        ], 
       
       }),
  }
</script>