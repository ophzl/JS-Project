<template>
  <div>
    <form class="mt-3" @submit.prevent="login">
      <div class="container">
        <div class="row justify-content-center">
          <div class="col-lg-6">
            <div class="card bg-light">
              <div class="card-body">
                <h3 class="font-weight-light mb-3">Se connecter</h3>
                <section class="form-group">
                  <div class="col-12 alert alert-danger px-3" v-if="error">{{ error }}</div>
                  <label class="form-control-label sr-only" for="Email">Email</label>
                  <input
                    required
                    class="form-control"
                    type="email"
                    id="email"
                    placeholder="Email"
                    v-model="email"
                  />
                </section>
                <section class="form-group">
                  <input
                    required
                    class="form-control"
                    type="password"
                    placeholder="Mot de passe"
                    v-model="password"
                  />
                </section>
                <div class="form-group text-right mb-0">
                  <button class="btn btn-primary" type="submit">Se connecter</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </form>
    <p class="text-center mt-2">
      ou
      <router-link to="/register">s'incrire</router-link>
    </p>
  </div>
</template>

<script>/* eslint-disable */
import Firebase from 'firebase'

export default {
  data: function () {
    return {
      email: '',
      password: '',
      error: ''
    }
  },
  methods: {
    // Login function with firebase authentication
    login: function () {
      const info = {
        email: this.email,
        password: this.password
      }
      Firebase.auth()
        .signInWithEmailAndPassword(info.email, info.password)
        .then(
          () => {
            this.$router.push('/')
          },
          error => {
            this.error = error.message
          }
        )
    }
  }
}
</script>
<style scoped>
</style>
