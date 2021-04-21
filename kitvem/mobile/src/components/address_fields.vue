<template>
  <div>
    <q-field>
      <q-input
        type="text"
        maxlength="8"
        v-model="cep"
        label="Informe o CEP"
        autofocus
      />
    </q-field>

    <div v-show="showAddressFields">
      <q-field>
        <q-input
          type="text"
          v-model="data.address"
          label="Informe o logradouro"
        />
      </q-field>

      <q-field>
        <q-input
          type="text"
          v-model="data.number"
          label="Informe o número"
        />
      </q-field>

      <q-field>
        <q-input
          type="text"
          v-model="data.complement"
          label="Informe o complemento"
        />
      </q-field>

      <q-field>
        <q-input
          type="text"
          v-model="data.neiborhood"
          label="Informe a bairro"
        />
      </q-field>

      <q-field>
        <q-input
          type="text"
          v-model="data.city"
          label="Informe o cidade"
        />
      </q-field>

      <q-field>
        <q-input
          type="text"
          v-model="data.state"
          label="Informe o estado"
        />
      </q-field>
    </div>
  </div>
</template>

<script>
export default {
  props: ['value'],
  data() {
    return {
      cep: this.value !== undefined ? this.value.cep || null : null,
      data: this.value || {},
      showAddressFields: false,
    };
  },
  watch: {
    cep(newValue) {
      if (newValue.length === 8) {
        this.data.cep = newValue;
        this.$emit('input', this.data);
        this.showAddressFields = true;
      } else {
        this.showAddressFields = false;
      }
    },
    data(newValue) {
      this.$emit('input', newValue);
    },
  },
  mounted() {
    if (this.cep !== null && this.cep.length === 8) {
      this.showAddressFields = true;
    }
  },
};
</script>

<style>
</style>
