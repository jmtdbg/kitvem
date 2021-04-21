<template>
  <q-page padding class="q-px-xl q-py-md">
    <h1 class="text-h3">
      Cadastre seu prato
    </h1>

    <form @submit.prevent="submit()" class="row q-gutter-md">
      <div class="col-12">
        <q-input
          type="text"
          v-model="data.title"
          label="Nome do prato"
          autofocus>
          <template v-slot:prepend>
            <q-icon name="label" />
          </template>
        </q-input>
      </div>

      <div class="col-12">
        <q-input
          type="text"
          v-model="data.photo"
          label="Foto do prato">
          <template v-slot:prepend>
            <q-icon name="insert_photo" />
          </template>
        </q-input>
      </div>

      <div class="col-12">
        <q-input
          type="text"
          v-model="data.description"
          label="Descrição do prato">
          <template v-slot:prepend>
            <q-icon name="description" />
          </template>
        </q-input>
      </div>
      <div class="col-6">
        <q-input
          type="text"
          v-model="data.price"
          label="Valor do prato">
          <template v-slot:prepend>
            <q-icon name="attach_money" />
          </template>
        </q-input>
      </div>

      <div class="col-12">
        <q-card>
          <q-card-section>
            <div class="text-h5">
              Opções do prato
            </div>
            <q-banner
              v-if="options.length === 0"
              inline-actions
              rounded
              class="q-mt-md bg-orange text-white">
                Nenhuma opção para esse prato
            </q-banner>
            <ul v-show="options.length > 0">
              <li class="q-my-sm" v-for="(opt, i) in options" :key="i">
                <q-btn size="sm" color="red" @click="optionsDelete(i)">x</q-btn> {{ opt }}
              </li>
            </ul>
            <q-input
              type="text"
              v-model="optionLabel"
              label="Adicionar para o prato">
              <template v-slot:prepend>
                <q-icon name="exposure_plus_1" />
              </template>
            </q-input>
            <q-btn color="primary" class="q-mt-md" @click="optionsAdd()">Adicionar</q-btn>
          </q-card-section>
        </q-card>
      </div>

      <div class="col">
        <q-btn type="submit" color="primary" class="q-my-md q-mr-sm">Salvar</q-btn>
        <q-btn type="submit" color="secondary"
          class="q-my-md" to="/restaurant/1/detail">Voltar</q-btn>
      </div>
    </form>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      data: {},
      options: [],
      optionLabel: null,
    };
  },
  methods: {
    submit() {
      this.$q.notify({
        message: 'Prato adicionado com sucesso',
        type: 'positive',
      });
    },
    optionsDelete(i) {
      this.options.splice(i, 1);
    },
    optionsAdd() {
      if (this.optionLabel === null) {
        this.$q.notify({
          message: 'Por favor, informe um título para a opção!',
        });
        return;
      }
      this.options.push(this.optionLabel);
      this.optionLabel = null;
    },
  },
};
</script>

<style>
</style>
