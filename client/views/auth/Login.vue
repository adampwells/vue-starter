<template>
<div class="content has-text-centered">
  <h1 class="is-title is-bold">Login</h1>

  <div class="columns is-vcentered">
    <div class="column is-6 is-offset-3">
      <div class="box">
        <div v-show="error" style="color:red; word-wrap:break-word;">{{ error }}</div>
        <form v-on:submit.prevent="login">
          <label class="label">Email</label>
          <p class="control">
            <input v-model="data.body.username" class="input" type="text" placeholder="email@example.org">
          </p>
          <label class="label">Password</label>
          <p class="control">
            <input v-model="data.body.password" class="input" type="password" placeholder="password">
          </p>

          <hr>
          <p class="control">
            <button type="submit" class="button is-primary">Login</button>
            <button class="button is-default">Cancel</button>
          </p>
        </form>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {

  data () {
    return {
      data: {
        body: {
          username: null,
          password: null
        },
        rememberMe: false
      },
      error: null
    }
  },
  mounted () {
    // Can set query parameter here for auth redirect or just do it silently in login redirect.
    if (window.localStorage) {
      let s = window.localStorage.getItem('session')
      if (s) {
        this.$store.commit('loggedIn', {'username': this.data.body.username})
        this.$router.push('/')
      }
    }
  },
  methods: {
    login () {
      this.$store.commit('loggedIn', {'username': this.data.body.username})
      this.$router.push('/')
      if (window.localStorage) {
        window.localStorage.setItem('session', {'username': this.data.body.username})
      }
    }
  }

}
</script>

<style lang="scss" scoped>
.is-title {
    text-transform: capitalize;
}
</style>
