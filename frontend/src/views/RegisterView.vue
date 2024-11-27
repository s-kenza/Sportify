<script>
import axios from "axios";

export default {
  data() {
    return {
      username: "",
      email: "",
      password: "",
    };
  },

  methods: {
    async register() {
      try {
        await axios({
          baseURL: import.meta.env.VITE_BACKENDURL,
          method: "post",
          url: "/user/register",
          data: {
            username: this.username,
            email: this.email,
            password: this.password,
          },
        });
      } catch (e) {
        console.log(e);
      }

      await this.$router.push({
        path: "/login",
      });
    },

    // test() {
    //   console.log();
    // },
  },
};
</script>

<template>
  <main>
    <form
      class="form-control w-full max-w-xs mx-auto my-32 gap-4"
      @submit.prevent="register"
    >
      <div>
        <label class="label">
          <span class="label-text">Pseudo :</span>
        </label>
        <input
          type="text"
          placeholder="Écrire ici"
          class="input input-bordered w-full max-w-xs"
          v-model="username"
        />
      </div>
      <div>
        <label class="label">
          <span class="label-text">E-mail :</span>
        </label>
        <input
          type="email"
          placeholder="Écrire ici"
          class="input input-bordered w-full max-w-xs"
          v-model="email"
        />
      </div>
      <div>
        <label class="label">
          <span class="label-text">Mot de passe :</span>
        </label>
        <input
          type="password"
          placeholder="Écrire ici"
          class="input input-bordered w-full max-w-xs"
          v-model="password"
        />
      </div>

      <button type="submit" class="btn btn-outline btn-primary w-full">
        S'inscrire
      </button>

      <small class="text-right text-xs"
        >Déjà un compte ? Se connecter
        <router-link to="/login" class="text-primary hover:underline"
          >Ici</router-link
        >.</small
      >
    </form>
  </main>
</template>
