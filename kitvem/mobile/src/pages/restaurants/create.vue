<template>
  <q-page padding class="q-px-xl q-py-md">
    <h1 class="text-h3">
      Cadastre seu restaurante
    </h1>

    <form @submit.prevent="submit()" class="row q-col-gutter-md">
      <div class="col-12">
        <q-input
          type="text"
          v-model="data.title"
          label="Nome do restaurante"
          autofocus
          clearable
          maxlength="80"
          >
          <template v-slot:prepend>
            <q-icon name="label" />
          </template>
        </q-input>
      </div>

      <div class="col-12">
        <q-input
          type="text"
          v-model="data.photo"
          label="Foto do restaurante">
          <template v-slot:prepend>
            <q-icon name="insert_photo" />
          </template>
        </q-input>
      </div>

      <div class="col-xs-12 col-sm-6 col-md-4">
          <q-input
            type="text"
            v-model="data.delivery_time"
            label="Tempo de entrega">
            <template v-slot:prepend>
              <q-icon name="timer" />
            </template>
          </q-input>
      </div>

      <div class="col-xs-12 col-sm-6 col-md-4">
        <q-input
          type="text"
          v-model="data.delivery_price"
          label="Valor de entrega">
          <template v-slot:prepend>
            <q-icon name="attach_money" />
          </template>
        </q-input>
      </div>

      <div class="col-12">
        <h2 class="text-h4">Endereço</h2>
        <address-fields v-model="address"></address-fields>
      </div>

      <div class="col">
        <q-btn type="submit" color="primary" class="q-my-md q-mr-sm">Salvar</q-btn>
        <q-btn type="submit" color="secondary" class="q-my-md" to="/restaurants">Voltar</q-btn>
       </div>
    </form>
  </q-page>
</template>

<script>
import AddressFields from '../../components/address_fields';

export default {
  data() {
    return {
      data: {},
      address: {},
    };
  },
  components: {
    'address-fields': AddressFields,
  },
  watch: {
    // address(newValue) {
    //   console.log(newValue);
    // },
  },
  methods: {
    submit() {
      this.$q.notify({
        message: 'Restaurante adicionado com sucesso',
        type: 'positive',
      });
    },
  },
};
</script>

<style>
</style>
