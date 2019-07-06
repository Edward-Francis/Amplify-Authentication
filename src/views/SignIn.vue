<template>
  <div class="sign-in">
    <h1>Sign In</h1>
    <v-form v-model="valid" ref="form" lazy-validation>
      <v-text-field
        v-model="username"
        :rules="emailRules"
        label="Email Address"
        required
      />
      <v-text-field
        v-model="password"
        :append-icon="passwordVisable ? 'visibility' : 'visibility_off'"
        :rules="[passwordRules.required, passwordRules.min]"
        :type="passwordVisable ? 'text' : 'password'"
        name="password"
        label="Password"
        hint="At least 8 characters"
        counter
        @click:append="passwordVisable = !passwordVisable"
        required
      />
      <v-btn :disabled="!valid" @click="submit">Submit</v-btn>
    </v-form>
  </div>
</template>

<script>
import { signIn } from "@/utils/auth.js";
export default {
  name: "SignIn",
  data() {
    return {
      valid: false,
      username: "",
      password: "",
      passwordVisable: false
    };
  },
  computed: {
    emailRules() {
      return [
        v => !!v || "E-mail is required",
        v => /.+@.+/.test(v) || "E-mail must be valid"
      ];
    },
    passwordRules() {
      return {
        required: value => !!value || "Required.",
        min: v => v.length >= 8 || "Minimum of 8 characters",
        emailMatch: () => "The email and password you entered don't match"
      };
    }
  },
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        console.log(
          "SIGN IN username: ${this.username}, password: ${this.password}"
        );
        signIn(this.username, this.password);
      }
    }
  }
};
</script>
