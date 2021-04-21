<template>
  <q-page padding>
    <h1 class="q-display-2">
      Pedido johnny
    </h1>
    <q-stepper ref="stepper" v-model="step" active-color="green" animated>
      <q-step
        :name="1"
        title="Forma de pagamento"
        icon="access_time"
        :done="step > 0"
      >
        <h5 class="text-center">Qual a forma de pagamento?</h5>
        <p class="text-center">
          <q-btn label="Escolher" color="primary" @click="payment_form=true"/>
        </p>
      </q-step>

      <q-step
        :name="2"
        title="Pedido recebido"
        icon="access_time"
        :done="step > 1"
      >
        <h5 class="text-center">Aguarde a confirmação do restaurante?</h5>
      </q-step>

      <q-step
        :name="3"
        title="Confirmação do restaurante"
        icon="access_time"
        :done="step > 2"
      >
        <h5 class="text-center">Pedido confirmado</h5>
        <p class="text-center">
          Estamos preparando o seu pedido, ele deve ser entrega a partir de 40 minutos.
        </p>
      </q-step>

      <q-step
        :name="4"
        title="Saiu para entrega"
        icon="access_time"
        :done="step > 3"
      >
        <h5 class="text-center">O entregador está a caminho</h5>
        <p class="text-center">
          Fique de olho no seu celular, o entregador pode precisar de informações.
        </p>
      </q-step>

      <q-step
        :name="5"
        title="Entregue"
        icon="access_time"
        :done="step > 4"
      >
        <h5 class="text-center">Bom apetite!</h5>
      </q-step>
      <template v-slot:navigation>
        <q-stepper-navigation>
          <q-btn flat @click="$refs.stepper.previous()" label="Volta"/>
          <q-btn flat @click="$refs.stepper.next()" label="Avança"/>
        </q-stepper-navigation>
      </template>
    </q-stepper>

    <q-dialog v-model="payment_form" content-classes="q-pa-md" :no-backdrop-dismiss="true">
      <q-card>
        <q-card-section>
          <div class="text-h5">Forma de pagamento</div>
        </q-card-section>

        <q-separator />

        <q-card-section style="max-height: 50vh" class="scroll">
          <q-radio v-model="payment" val="1" label="Dinheiro"/><br>
          <q-radio v-model="payment" val="2" label="Cartão de Crédito"/><br>
          <q-radio v-model="payment" val="3" label="Cartão de Débito"/>
        </q-card-section>

        <q-separator />

        <q-card-actions align="right">
          <!-- <q-btn flat label="Decline" color="primary" v-close-popup /> -->
          <div class="q-pa-md q-gutter-md">
            <div v-if="payment === '1'">
              <q-input
                filled
                stack-label
                type="text"
                v-model="change"
                label="Troco para?"
                mask="#.##"
                fill-mask="0"
                reverse-fill-mask
                hint="R$: #.##"
                input-class="text-right"
              />
            </div>
            <div>
            <q-btn
              label="Confirmar pedido?"
              color="primary"
              class="q-mt-sm"
              @click="pay()"
            />
          </div>
          </div>
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      payment_form: true,
      payment: '1',
      change: 0.00,
      step: 1,
    };
  },
  methods: {
    pay() {
      this.payment_form = false;
      this.$refs.stepper.next();
    },
  },
};
</script>

<style>
</style>
