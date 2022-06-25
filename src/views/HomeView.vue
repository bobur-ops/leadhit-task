<template>
  <div class="row">
    <div class="col s6 offset-s3">
      <h1>LeadHit</h1>
      <form @submit.prevent="submitHandler">
        <div class="input-field">
          <input
            v-model="siteId"
            @input="clearError"
            id="last_name"
            type="text"
            class="validate"
          />
          <label for="last_name">ID</label>
        </div>
        <div v-if="idLengthError" class="red-text text-accent-4">
          id сайта должен содержать 24 символа
        </div>
        <button class="btn" type="submit">Войти</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HomeView",
  data() {
    return {
      siteId: "",
      idLengthError: false,
    };
  },
  mounted() {
    if (localStorage.getItem("leadhit-site-id")) {
      this.$router.push("/analytics");
    }
  },
  methods: {
    async submitHandler() {
      if (this.siteId.length !== 24) {
        this.idLengthError = true;
        this.siteId = "";
      } else {
        const url = "https://track-api.leadhit.io/client/test_auth";
        const config = {
          headers: {
            "Api-Key": "5f8475902b0be670555f1bb3:eEZn8u05G3bzRpdL7RiHCvrYAYo",
            "Leadhit-Site-Id": this.siteId,
          },
        };

        axios
          .get(url, config)
          .then((res) => {
            if (res.data.message === "ok") {
              localStorage.setItem(
                "leadhit-site-id",
                "5f8475902b0be670555f1bb3"
              );

              this.$router.push("/analytics");
            }
          })
          .catch((err) => console.log(err));
      }
    },
    clearError() {
      this.idLengthError = false;
    },
  },
};
</script>
