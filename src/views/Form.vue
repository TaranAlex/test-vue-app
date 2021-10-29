<template>
  <div class="about">
    <h1>Test Vee-Validate</h1>
    <div>
      <ValidationObserver ref="form" v-slot="{ invalid }">
        <ValidationProvider rules="required|even" name="Четное число">
          <div slot-scope="{ errors }">
            <input v-model="num_value" type="number" placeholder="Введите четное число">
            <p>{{ errors[0] }}</p>
          </div>
        </ValidationProvider>
        <ValidationProvider name="Имя" rules="required|alpha|min:2|max:5">
          <div slot-scope="{ errors }">
            <input v-model="name" placeholder="Введите имя">
            <p>{{ errors[0] }}</p>
          </div>
        </ValidationProvider>
        <ValidationProvider name="Емейл" rules="required|email">
          <div slot-scope="{ errors }">
            <input v-model="email" placeholder="Введите Емейл">
            <p>{{ errors[0] }}</p>
          </div>
        </ValidationProvider>
      </ValidationObserver>
      <button type="button" @click="send">Submit</button>
    </div>
  </div>
</template>

<script>
import {extend} from 'vee-validate';

extend('even', value => {
  return value % 2 === 0;
});

export default {
  data: () => ({
    num_value: '',
    name: '',
    email: '',
  }),
  methods: {
    send() {
      this.$refs.form.validate().then(ok => {
        ok ? alert('Submit!') : alert('fix errors!');
      })
    }
  }
}
</script>
