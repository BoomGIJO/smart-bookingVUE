<template>
  <v-parallax src="/pic/background.png" height="643">
    <v-card-media
      height="250"
      contain
      src="/pic/logo.png"
    />

    <v-card height="250" color="teal lighten-4">
      <form class="form-signin" @submit.prevent="login">
        <h2 class="form-signin-heading">Please sign in</h2>
        <input id="inputEmail" v-model="email" type="email" class="form-control" placeholder="Email address" required autofocus>
        <input id="inputPassword" v-model="password" type="password" class="form-control" placeholder="Password" required>
        <div class="text-xs-center">
          <v-btn color="orange" type="submit" >Sign in</v-btn>
          Or
          <nuxt-link to="/register">Sign Up </nuxt-link>
        </div>
      </form>
    </v-card>
    <v-snackbar
      v-model="snackbar"
      top
    >
      login failed
      <v-btn flat color="pink" @click.native="snackbar = false">Close</v-btn>
    </v-snackbar>

  </v-parallax>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      email: '',
      password: '',
      snackbar: false,
    }
  },
  methods: {
    async login () {
      let res = await this.$http.post('/login', {email: this.email, password: this.password})
      if (res.data.ok) {
        window.sessionStorage.setItem('user', JSON.stringify(res.data.user))
        this.$router.push('/booking')
      } else {
        this.snackbar = true
      }
      // console.log(this.password)
    },
  },
}
</script>

<style lang="css">
body {
  background: #605B56;
}

.login-wrapper {
  background: #fff;
  width: 70%;
  margin: 12% auto;
}

.form-signin {
  max-width: 330px;
  padding: 10% 15px;
  margin: 0 auto;
}
.form-signin .form-signin-heading,
.form-signin .checkbox {
  margin-bottom: 10px;
}
.form-signin .checkbox {
  font-weight: normal;
}
.form-signin .form-control {
  position: relative;
  height: auto;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  padding: 10px;
  font-size: 16px;
}
.form-signin .form-control:focus {
  z-index: 2;
}
.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>
