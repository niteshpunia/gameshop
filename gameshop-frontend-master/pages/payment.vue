<template>
  <!--MAIN-->
  <main>
    <!--Payment -->
    <div class="registerAddress mt-3">
      <div class="container-fluid c-section">
        <div class="row">
          <div class="col-sm-3"></div>
          <div class="col-sm-6">
            <div class="a-section a-spacing-medium">
            </div>
            <div class="a-section">
              <h2>Make a payment</h2>
              <div class="a-section a-spacing-none a-spacing-top-small">
                <b>The total price is {{getCartTotalPrice}}</b>
              </div>

              <form action="#" method="post">
                <div class="a-spacing-medium a-spacing-top-medium">
                  <div class="a-spacing-top-medium">
                    <!-- Stripe card -->
                    <div ref="card"></div>
                    <!-- End of Stripe card -->
                  </div>

                  <div class="a-spacing-top-medium"></div>
                  <hr />
                  <div class="a-spacing-top-medium">
                    <span>
                      <b>Make sure your address is correct</b>
                    </span>
                  </div>
                  <div>
                    <span>If the address contains typos or other errors, your package may be undeliverable.</span>
                  </div>

                  <!-- Purchase Button -->
                  <button @click="onPurchase">Purchase</button>
                </div>
              </form>
            </div>
          </div>
          <div class="col-sm-3"></div>
        </div>
      </div>
    </div>
    <!--/Payment ADDRESS-->
  </main>
  <!--/MAIN-->
</template>

<script>
import { mapGetters} from 'vuex';
export default {
  data(){
    return {
      error: "",
      stripe: null,
      card: null
    }
  },

  mounted(){
    this.stripe = Stripe("pk_test_51HmkvSAThxS0T2XkpUg68gVKtllFxjYKbwDlVbCf1lHZX3uHJRunoVSl25csVE4puQbpGtJogVFDXG8sRlJ0vCPM0024bcxgCk")
    let elements = this.stripe.elements();
    this.card = elements.create("card");
    this.card.mount(this.$refs.card);
  },

  methods: {
    async onPurchase(e){
      e.preventDefault();
      try{
        let token = await this.stripe.createToken(this.card);
        let response = await this.$axios.$post('http://localhost:5000/payment/makePayment', {
          token: token,
          totalPrice: this.getCartTotalPrice,
          cart: this.getCart
        });

        if(response.success){
          this.$store.commit("clearCart");
          this.$router.push("/");
        }
      }catch(err){
        console.log(err);
      }
    }
  },

  computed: {
    ...mapGetters(["getCart", "getCartTotalPrice"])
  }

}

</script>

<style scoped>
.StripeElement {
  box-sizing: border-box;
  height: 40px;
  padding: 10px 12px;
  border: 1px solid transparent;
  border-radius: 4px;
  background-color: white;
  box-shadow: 0 1px 3px 0 #e6ebf1;
  -webkit-transition: box-shadow 150ms ease;
  transition: box-shadow 150ms ease;
}

.StripeElement--focus {
  box-shadow: 0 1px 3px 0 #cfd7df;
}

.StripeElement--invalid {
  border-color: #fa755a;
}

.StripeElement--webkit-autofill {
  background-color: #fefde5 !important;
}
</style>
