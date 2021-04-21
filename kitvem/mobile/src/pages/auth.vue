<template>
  <q-page padding class="q-px-xl q-py-md">
    <h1 class="text-h3 text-center">
      Identificação
    </h1>
    <div class="q-pa-md row items-start q-gutter-md justify-center">

      <div class="col-12 col-md-5">
        <q-card>
          <q-card-section>
            <form @submit.prevent="auth()">
              <p class="caption">Já tenho conta</p>
                <q-input
                  type="email"
                  v-model="dataLogin.email"
                  label="Email">
                  <template v-slot:prepend>
                    <q-icon name="email" />
                  </template>
                </q-input>
                <q-input
                  type="password"
                  v-model="dataLogin.password"
                  label="Senha">
                  <template v-slot:prepend>
                    <q-icon name="lock" />
                  </template>
                </q-input>

              <q-btn type="submit" color="primary" class="q-my-md">Acessar</q-btn>
              <!-- <q-btn color="primary" class="q-ma-md" @click="testar()">Testar</q-btn> -->

            </form>
          </q-card-section>
        </q-card>
      </div>

      <div class="col-12 col-md-5">
        <q-card>
          <q-card-section>
            <form @submit.prevent="register()">
              <p class="caption">Quero me cadastrar</p>
                <q-input
                  type="text"
                  v-model="dataRegister.name"
                  label="Name"
                  autofocus>
                  <template v-slot:prepend>
                    <q-icon name="label" />
                  </template>
                </q-input>
                <q-input
                  type="email"
                  v-model="dataRegister.email"
                  label="Email">
                  <template v-slot:prepend>
                    <q-icon name="email" />
                  </template>
                </q-input>
                <q-input
                  type="password"
                  v-model="dataRegister.password"
                  label="Senha">
                  <template v-slot:prepend>
                    <q-icon name="lock" />
                  </template>
                </q-input>
                <q-input
                  type="password"
                  v-model="dataRegister.passwordConfirmation"
                  label="Confirmação de senha">
                  <template v-slot:prepend>
                    <q-icon name="lock_open" />
                  </template>
                </q-input>

              <q-btn type="submit" color="primary" class="q-my-md">Cadastrar</q-btn>

            </form>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
import qs from 'qs';

export default {
  data() {
    return {
      dataLogin: {},
      dataRegister: {},
      token: null,
    };
  },
  methods: {
    // async testar() {
    //   const response = await this.$axios.get('/users/me.json', {
    //     headers: {
    //       Authorization: `Bearer ${this.token}`,
    //     },
    //   });
    //   console.log(response);
    // },
    async auth() {
      const data = qs.stringify(this.dataLogin);
      const response = await this.$axios.post('http://localhost:8000/api/login', data);

      const { token } = response.data.data;
      this.token = token;

      if (response.status === 200) {
        this.$q.notify({
          message: 'Autenticado com sucesso',
          type: 'positive',
        });
      }
    },
    async register() {
      if (!this.dataRegister.password
          || this.dataRegister.password !== this.dataRegister.passwordConfirmation) {
        this.$q.notify({
          message: 'As senhas não conferem',
        });
        return;
      }

      const data = qs.stringify(this.dataRegister);
      const response = await this.$axios.post('http://localhost:8000/api/register', data);

      if (response.status === 200) {
        this.$q.notify({
          message: 'Cadastrado com sucesso',
          type: 'positive',
        });
      }
    },
  },
};
</script>

<style>
</style>
