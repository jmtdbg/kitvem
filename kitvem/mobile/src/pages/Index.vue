<template>
  <q-page padding class="bg-food">
    <div class="flex flex-center">
      <h1 class="q-display-3 text-center text-grey-8 q-py-xl">Bem Vindo ao Kitcome</h1>
    </div>
    <div class="q-pa-md row items-start q-gutter-md justify-center">
      <div class="col-xs-12 col-md-3">
        <q-card dark bordered class="bg-positive my-card">
          <q-card-section>
            <div class="text-h6">
              <q-icon name="location_on"/>
              Usar minha localização atual
            </div>
            <div class="text-subtitle2">Ative o GPS</div>
          </q-card-section>
          <q-separator dark inset />
          <q-card-section>
            Próximo de ...
          </q-card-section>
          <q-card-actions>
            <q-btn to="/list-restaurants" flat label="Ver restaurantes"/>
          </q-card-actions>
        </q-card>
      </div>
      <div class="col-xs-12 col-md-3">
        <q-card dark bordered class="bg-orange-5 my-card">
          <q-card-section>
            <div class="text-h6">
              <q-icon name="account_box"/>
              Acessar sua conta</div>
            <div class="text-subtitle2">Login</div>
          </q-card-section>
          <q-separator dark inset />
          <q-card-section>
            Você pode pedir usando um endereço já existem acesse sua conta
            para começar
          </q-card-section>
          <q-card-actions>
            <q-btn to="/list-restaurants" flat label="Acessar conta"/>
          </q-card-actions>
        </q-card>
      </div>
      <div class="col-xs-12 col-md-3">
        <q-card dark bordered class="bg-light-blue-7 my-card">
          <q-card-section>
            <div class="text-h6">
            <q-icon name="fastfood"/> Escolher localização</div>
          </q-card-section>
          <q-separator dark inset />
          <q-card-section>
            <q-btn
              to="/list-restaurants"
              color="white"
              text-color="primary"
              size="md"
              class="q-mr-md q-mb-md"
              :label="place"
              v-for="(place, index) in places"
              :key="index"
            />
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<style>
/* .bg-food {
  background: url("~assets/quasar-logo-full.svg") no-repeat;
  background-size: contain;
} */
/* .my-card {
  width: 100%;
  max-width: 250px;
} */
</style>

<script>

export default {
  name: 'PageIndex',
  data() {
    return {
      places: [
        'CIDADE 1',
        'CIDADE 2',
        'BAIRRO 1',
        'BAIRRO 2',
        'BAIRRO 3',
      ],
    };
  },
};
</script>
