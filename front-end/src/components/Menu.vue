<template>
  <div id="menu">
    <nav class="navbar navbar-expand-lg justify-content-between">
        <div class="container">
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <div class="navbar-nav">
                    <router-link class="nav-link" to="/">Feed</router-link>
                    <router-link class="nav-link" to="/discover">Discover</router-link>
                    <router-link class="nav-link" to="/myposts">My Posts</router-link>
                    <router-link class="nav-link" to="/profile">My Profile</router-link>
                    <button class="pure-button nav-link pure-button-primary" v-if="user" @click="logout">Logout</button>
                </div>
            </div>
        </div>
    </nav>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Menu',
  props: {
    user: Object
  },
  methods: {
    async logout() {
      try {
        await axios.delete("/api/users");
        this.$root.$data.user = null;
      } catch (error) {
        this.$root.$data.user = null;
      }
    },
  }
}
</script>

<style scoped>
.nav-link, a {
  font-size: 1.5rem;
  color: #b7c1de;
}

.navbar {
  width: 100%;
  background-color: #0b468c;
  padding-bottom: 0;
  padding-top: 0;
  margin-bottom: 10px;
}
</style>
