/* eslint-disable consistent-return */
<template>
  <div class="container">
    <h2>hello</h2>

    <form class="col-lg-4 pt-5" @submit.prevent="formSubmit">
      <!-- Email -->
      <div class="form-group">
        <label for="email">Email</label>
        <input
          type="email"
          id="email"
          class="form-control"
          :class="{ 'is-invalid': $v.email.$error }"
          v-model="email"
          @blur="$v.email.$touch()"
        />
        <div class="invalid-feedback" v-if="!$v.email.required">email is required</div>
        <div class="invalid-feedback" v-if="!$v.email.email">email is incorrect</div>
        <div class="invalid-feedback" v-if="!$v.email.uniqueEmail">this email already exists</div>
      </div>

      <!-- Parol -->
      <div class="form-group">
        <label for="password">Password</label>
        <input
          type="password"
          id="password"
          class="form-control"
          :class="{ 'is-invalid': $v.password.$error }"
          v-model="password"
          @blur="$v.password.$touch()"
        />
        <div class="invalid-feedback" v-if="!$v.password.required">password is required</div>
        <div class="invalid-feedback" v-if="!$v.password.minLength">password is incorrect</div>
      </div>

      <!-- Confirm -->
      <div class="form-group">
        <label for="confirm">Confirm Password</label>
        <input
          type="password"
          id="confirm"
          class="form-control"
          :class="{ 'is-invalid': $v.confirmPassword.$error }"
          v-model="confirmPassword"
          @blur="$v.confirmPassword.$touch()"
        />
        <div class="invalid-feedback" v-if="!$v.confirmPassword.sameAs">
          password should match
        </div>
      </div>
      <button class="btn btn-success" type="submit" :disabled="$v.$invalid">Submit</button>
    </form>
  </div>
</template>

<script>
import {
  required, email, minLength, sameAs,
} from 'vuelidate/lib/validators';

export default {
  data() {
    return {
      email: '',
      password: '',
      confirmPassword: '',
    };
  },
  methods: {
    formSubmit() {
      console.log(this.email, this.password);
    },
  },
  validations: {
    email: {
      required,
      email,
      uniqueEmail: (unique) => unique !== 'mnjoyan@mail.ru',
    },
    password: {
      required,
      minLength: minLength(6),
    },
    confirmPassword: {
      required,
      sameAs: sameAs('password'),
    },
  },
};
</script>
