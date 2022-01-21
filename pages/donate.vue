<template>
    <div>
<v-container fill-height fluid>
    <v-row>
        <v-spacer></v-spacer>
        <v-col justify="center" align="center" xs="12" sm="12" md="6">
            <h1>donate</h1>
            <v-divider></v-divider>
            <h4 class="pt-5">Support us with a donation! <v-icon color="red">mdi-heart</v-icon>
If you donate only <strong>3 USD</strong> or more you will get all available HTTP, HTTPS, SOCKS4 and SOCKS5 proxies as CSV, JSON and TXT files.</h4>
<h4 class="pt-5">format IP:Port immediately. <v-icon>mdi-truck-fast</v-icon></h4>

  <v-card class="mt-10" color="light-green lighten-2">
    <v-tabs v-model="tab" background-color="transparent" color="basil" grow >
      <v-tab>Paypal</v-tab>
      <v-tab>Bitcoin</v-tab>
    </v-tabs>

    <v-tabs-items v-model="tab">
      <v-tab-item>
        <v-card color="basil" flat >
          <v-card-text>
            <form action="https://www.paypal.com/donate" method="post" target="_top">
<input type="hidden" name="hosted_button_id" value="CLUKLD46YHQU6" />
<input type="image" src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" border="0" name="submit" title="PayPal - The safer, easier way to pay online!" alt="Donate with PayPal button" />
<img alt="" border="0" src="https://www.paypal.com/en_AR/i/scr/pixel.gif" width="1" height="1" />
</form>
</v-card-text>
        </v-card>
      </v-tab-item>
    <v-tab-item>
        <v-card color="basil" flat >
          <v-card-text>
              <h3>bc1qyt8hkwycnn54n2xqjdxl0pl656wcr8sjv4rexg</h3>
              <v-img class="mt-2" max-width="150px" src="btcwallet.png"></v-img>
              </v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </v-card>

<h3 class="mt-10">Thanks for your support! <v-icon color="blue">mdi-robot-happy</v-icon></h3>

        </v-col>
        <v-spacer></v-spacer>
    </v-row>
</v-container>
    </div>
</template>

<script>
    export default {
        data() {
            this.pk = process.env.STRIPE_PK;
            return {
            tab: null,
            items: ['Paypal', 'Stripe', 'Bitcoin', 'MercadoPago'],
            text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
                lineItems: [
                {
                price: 'price_1IQVKrBGCvawhmKDtaXQPy79',
                quantity: 1,
                },
                ],
            }
        },
        methods: {
        checkout () {
            this.$refs.checkoutRef.redirectToCheckout();
    },
  },
    }
</script>

<style>
/* Helper classes */
.basil {
  background-color: #FFFBE6 !important;
}
.basil--text {
  color: #356859 !important;
}
</style>