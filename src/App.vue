<template>
  <v-app id="inspire">
    <v-navigation-drawer 
    v-model="drawer"
    app
    >
    
      <v-list-item class="px-2">
        <v-list-item-avatar>
          <v-img src="../src/assets/FlameLogo.png"></v-img>
        </v-list-item-avatar>

        <v-list-item-title>Flame</v-list-item-title>
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
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="primary"
      dense
      dark
      src="../src/assets/city.jpg"
      prominent
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
        ></v-img>
      </template>

      <v-col
          cols="12"
          sm="1"
      >
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      </v-col>
      <v-divider
      class="mx-2"
      vertical
    ></v-divider>
      <v-col
          cols="12"
          sm="10"
      >
      <v-app-bar-title>Flame</v-app-bar-title>
      </v-col>
      <v-col
          cols="12"
          sm="1"
      >
      <v-btn icon @click.prevent="logOut">
        <v-icon>mdi-logout-variant</v-icon>
      </v-btn>
      </v-col>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>


<script>

export default {
      data: () => ({ 
      drawer: null,
      items: [
          { title: 'Home', icon: 'mdi-home-circle-outline', to:'/' },
          { title: 'Board Admin', icon: 'mdi-head-minus-outline', to:'/admin' },
          { title: 'Board Moderator', icon: 'mdi-head-cog-outline', to:'/mod' },
          { title: 'Board User', icon: 'mdi-account-group-outline', to:'/user' },
          { title: 'Profile', icon: 'mdi-account-details', to:'/profile' },
          { title: 'Campaigns', icon: 'mdi-account-details', to:'/campaigns' },
          { title: 'Create Campaign', icon: 'mdi-briefcase-plus-outline', to:'/createcampaign' },
          { title: 'About Us', icon: 'mdi-information', to:'/about' },
        ]
      }),
  computed: {
    currentUser() {
      return this.$store.state.auth.user;
    },
    showAdminBoard() {
      if (this.currentUser && this.currentUser.roles) {
        return this.currentUser.roles.includes('ROLE_ADMIN');
      }

      return false;
    },
    showModeratorBoard() {
      if (this.currentUser && this.currentUser.roles) {
        return this.currentUser.roles.includes('ROLE_MODERATOR');
      }

      return false;
    }
  },
  methods: {
    logOut() {
      this.$store.dispatch('auth/logout');
      this.$router.push('/login');
    }
  }
};
</script>