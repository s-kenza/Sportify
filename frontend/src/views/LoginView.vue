<script>
import axios from "axios";
import { useUserStore } from "@/stores/user";

export default {
  setup() {
    const userStore = useUserStore();
    return { userStore };
  },

  data() {
    return {
      email: "",
      password: "",
    };
  },

  methods: {
    async login() {
      try {
        const token = await axios({
          baseURL: import.meta.env.VITE_BACKENDURL,
          method: "post",
          url: "/user/login",
          data: {
            email: this.email,
            password: this.password,
          },
        });
        await this.userStore.setToken(token.data);
        window.location.reload(); // Rafraîchir la page pour mettre à jour les données
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>

<template>
  <main>
    <form
      class="form-control w-full max-w-xs mx-auto my-40 gap-4"
      @submit.prevent="login"
    >
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

      <button class="btn btn-outline btn-primary w-full">Se connecter</button>

      <small class="text-right text-xs"
        >Pas de compte ? S'inscrire
        <router-link to="/register" class="text-primary hover:underline"
          >Ici</router-link
        >.</small
      >
    </form>
  </main>
</template>
