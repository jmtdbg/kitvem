<template>
  <!-- <q-layout view="hHh Lpr lff"> -->
  <q-layout view="hHh lpR fFf">
    <q-header elevated>
      <q-toolbar class="bg-light-green-1 text-grey-8">
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title class="text-grey-8">
          Kitvem App
        </q-toolbar-title>
        <q-btn flat to="/cart">
          <transition enter-active-class="animated tada" leave-active-class="hidden">
            <q-chip icon="shopping_cart" :key="cart_count">{{ cart_count }}</q-chip>
          </transition>
        </q-btn>

        <!-- <div>Quasar v{{ $q.version }}</div> -->
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-amber-3"
      id="sidebar"
    >
      <q-list>
        <q-item-label
          header
          class="text-grey-8"
        >
        <q-item>
          <q-img src="~assets/quasar-logo-full.svg" alt=""></q-img>
        </q-item>
          Menu
        </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>
<style>
#sidebar .q-item.router-link-active {
  background: rgba(red, green, blue, 0.1);
}
#sidebar .q-item.q-link {
  background: rgba(red, green, blue, 0.2);
}
#sidebar .q-item img {
  width: 80%;
  height: auto;
}
</style>
<script>
import EssentialLink from 'components/EssentialLink.vue';

const linksData = [
  {
    title: 'Quero pedir',
    caption: 'Busque seus Kits e faça seu pedido',
    icon: 'local_grocery_store',
    link: '/',
  },
  {
    title: 'Tenho uma Loja',
    caption: 'Cadastre sua loja e receba kits de produtos',
    icon: 'add_business',
    link: '/restaurants',
  },
  {
    title: 'Tenho uma fazenda/sítio',
    caption: 'Cadastre sua fazenda/sítio e receba pedidos',
    icon: 'agriculture',
    link: '/restaurants',
  },
  {
    title: 'Meus Pedidos',
    caption: 'Acompanhe seus pedidos',
    icon: 'electric_moped',
    link: '/orders',
  },
  {
    title: 'Login',
    caption: 'Acesse sua conta',
    icon: 'account_box',
    link: '/auth',
  },
];

export default {
  name: 'MainLayout',
  components: { EssentialLink },
  data() {
    return {
      leftDrawerOpen: false,
      essentialLinks: linksData,
      cart_count: 0,
    };
  },
  // methods: {
  //   openURL,
  // },
  watch: {
    cart_count(newValue, oldValue) {
      if (newValue > oldValue) {
        this.$q.notify({
          message: 'Pedido atualizado?',
          detail: 'Um novo item foi adicionado ao seu pedido, quer ir para o carrinho de compras?',
          type: 'positive',
          actions: [
            {
              label: 'Ver pedido',
              handler: () => {
                this.$router.push('/cart');
              },
            },
          ],
        });
      }
    },
  },
  mounted() {
    setTimeout(() => {
      this.cart_count += 1;
    }, 1000);

    setTimeout(() => {
      this.cart_count += 1;
    }, 5000);
  },
};
</script>
