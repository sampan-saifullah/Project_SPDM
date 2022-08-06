<template>
  <div>
    <v-row>
      <v-col class="d-flex" cols="6">
        <v-card class="mx-auto" max-width="344">
          <v-card-text>
            <div>Login Form</div>
            <v-text-field
              label="Email"
              v-model="email"
              hide-details="auto"
            ></v-text-field>
            <v-text-field
              label="Password"
              v-model="password"
              type="password"
            ></v-text-field>
          </v-card-text>
          <v-card-actions>
            <v-btn
              text
              color="teal accent-4"
              @click="goLogin"
              :disabled="!email || !password"
              :loading="loading"
            >
              Login
            </v-btn>
            {{ msg }}
          </v-card-actions>
        </v-card>
      </v-col>
      <v-col class="d-flex" cols="6">
        <v-card class="mx-auto" max-width="344">
          <v-card-text>
            <div>Signup Form</div>
            <v-text-field
              label="Name"
              v-model="name"
              hide-details="auto"
            ></v-text-field>
            <v-text-field
              label="Email"
              v-model="emailS"
              hide-details="auto"
            ></v-text-field>
            <v-text-field
              label="Password"
              v-model="passwordS"
              type="password"
            ></v-text-field>
          </v-card-text>
          <v-card-actions>
            <v-btn
              text
              color="teal accent-4"
              @click="goSignup"
              :disabled="!emailS || !passwordS"
              :loading="loading"
            >
              Signup
            </v-btn>
            {{ msg2 }}
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      emailS: "",
      passwordS: "",
      loading: false,
      msg: "",
      msg2: "",
      name: "",
    };
  },
  methods: {
    goSignup() {
      this.loading = true;
      const that = this;
      this.$axios
        .post("/signup", {
          email: this.emailS,
          password: this.passwordS,
          name: this.name,
        })
        .then(function (response) {
          that.loading = false;
          that.msg2 = response.data.msg;
          console.log(response.data);
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    goLogin() {
      this.loading = true;
      const that = this;
      this.$axios
        .post("/login", {
          email: this.email,
          password: this.password,
        })
        .then(function (response) {
          that.loading = false;
          that.msg = response.data.msg;
          console.log(response.data);
          if (that.msg === "Success") {
            that.$router.push("/create");
          }
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
};
</script>

<style>
</style>