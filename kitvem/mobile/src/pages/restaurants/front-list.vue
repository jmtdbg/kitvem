<template>
  <q-page padding class="q-px-xl q-py-md">
    <h1 class="text-h3">
      <q-icon name="location_on"/> Restaurantes próximos a você asaph
    </h1>
    <p><span class="text-grey">Caraguatatuba </span></p>
    <p><q-btn to="/" color="primary" label="Trocar localização"/></p>
    <div class="row q-gutter-lg">
      <div class="col-xs-6 col-md-5" v-for="i in 6" :key="i">
        <q-card>
          <q-card-media>
            <q-img src="~assets/food.jpg"></q-img>
            <q-card-section slot="overlay">
              Nome do restaurante
              <span slot="subtitle">Entrega em 30-40 min</span>
            </q-card-section>
          </q-card-media>
          <q-separator/>
          <q-card-section>
            <q-icon name="star" v-for="i in star_range(2.5).full" :key="i"/>
            <q-icon name="star_half" v-for="i in star_range(2.5).half" :key="i*5"/>
            <q-icon name="star_border" v-for="i in star_range(2.5).empty" :key="i*10"/>
          </q-card-section>
          <q-card-actions>
            <q-btn to="/restaurant/1" flat color="primary" label="Ver cardápio"/>
          </q-card-actions>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  methods: {
    star_range(rate) {
      const full = Math.trunc(rate);
      let half = 0;

      if (rate % 1 !== 0) {
        half = 1;
      }

      const empty = 5 - (full + half);

      return {
        full,
        half,
        empty,
      };
    },
  },
};
</script>

<style>
</style>
