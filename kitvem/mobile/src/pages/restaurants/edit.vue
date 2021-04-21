<template>
  <q-page padding class="q-px-xl q-py-md">
    <h1 class="text-h3">
      Editando restaurante
    </h1>

    <form @submit.prevent="submit()" class="row q-col-gutter-md">
      <div class="col-12">
        <q-field>
          <template v-slot:prepend>
            <q-icon name="label" />
          </template>
          <q-input
            type="text"
            v-model="data.title"
            label="Nome do restaurante"
            autofocus/>
        </q-field>
      </div>

      <div class="col-12">
        <q-field>
          <template v-slot:prepend>
            <q-icon name="insert_photo" />
          </template>
          <q-input
            type="text"
            v-model="data.photo"
            label="Foto do restaurante"/>
        </q-field>
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
        <h2 class="q-display-1">Endereço</h2>
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
      data: {
        title: 'Nome do resstaurante',
        delivery_time: '10 minutos',
        delivery_price: '10,00',
      },
      address: {
        cep: '11676085',
        address: 'R. Fulano',
        number: '123',
        complement: 'Casa',
        neiborhood: 'Centro',
        city: 'Caraguatatuba',
        state: 'SP',
      },
    };
  },
  components: {
    'address-fields': AddressFields,
  },
  methods: {
    submit() {
      this.$q.notify({
        message: 'Restaurante alterado com sucesso',
        type: 'positive',
      });
    },
  },
};
</script>

<style>
</style>
