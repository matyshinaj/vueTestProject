<template>
  <div
    id="app"
    class="bg-no-repeat bg-cover bg-white hero relative"
    :style="{ backgroundImage: `url(${backgroundUrl})` }"
  >
    <div class="ccbox" v-if="isCheckoutCompleted">
      <div class="cbox">
        <p>Thanks for shopping with us!</p>
      </div>
    </div>
    <div class="ccbox" v-if="!isCheckoutCompleted">
      <Basket :data="items" :update="updateCart" :remove="deleteItem"/>
      <SummaryBox :data="summary" @completed="checkoutCompleted" />
    </div>
    <Logo />
  </div>
</template>
<script>
import Logo from "./components/Logo.vue";
import Basket from "./components/Basket.vue";
import backgroundUrl from "./assets/bg.jpg";
import SummaryBox from './components/Summary.vue';

export default {
  name: "app",
  components: {
    Logo,
    Basket,
    SummaryBox,
  },
  methods: {
    summaryUpdate() {
      let sum = 0;
      for (let i = 0; i < this.items.length; i++) {
        sum += this.items[i].price * this.items[i].quantity;
      }
      this.summary.itotal = sum * 0.9;
      this.summary.tax = sum * 0.1;
      this.summary.shipping = sum * 0.15;
      this.summary.subtotal = this.summary.shipping + sum;
    },
    updateCart(item, updateType) {    
      for (let i = 0; i < this.items.length; i++) {
        if (this.items[i].id === item.id) {
          if (updateType === 'sub') {
            if (this.items[i].quantity !== 0) {
              this.items[i].quantity--;
            }
          } else if (this.items[i].quantity < 9) {
            this.items[i].quantity++;
          }      
          break;
        }
      }
      this.summaryUpdate();
    },
    deleteItem(item) {
      for (let i = 0; i < this.items.length; i++) {
        if (this.items[i].id === item.id) {
          this.items.splice(i, 1);
          break;
        }
      }
      this.summaryUpdate();
    },
    checkoutCompleted() {
      this.isCheckoutCompleted = true;
    }
  },
  data() {
    return {
      isCheckoutCompleted: false,
      backgroundUrl,
      items: [
                {
                    id: 1,
                    title: 'Product A',
                    price: 24,
                    quantity: 0,
                },
                {
                    id: 2,
                    title: 'Product B',
                    price: 19.99,
                    quantity: 0,
                },
                {
                    id: 3,
                    title: 'Product C',
                    price: 29.96,
                    quantity: 0,
                },
            ],
      summary : {
        itotal: 0,
        tax: 0,
        shipping: 0,
        subtotal: 0,
      }
    };
  },
};
</script>
<style lang="scss">
@import "~@/assets/scss/vendors/bootstrap-vue/index";
html,
body,
#app {
  height: 100%;
  width: 100%;
  background: white;
  margin: 0px;
  display: flex;
}
.cbox {
    width: 300px;
    height: fit-content;
    margin: auto auto;
    background: #FFFFFF;
    box-shadow: 1px 2px 3px 0px rgba(0,0,0,0.10);
    border-radius: 6px;
    display: flex;
    flex-direction: column;
    p {
      text-align: center;
      margin-bottom: 0px;
      padding: 1rem;
      background-color: #d1e7de;
      color: #205e41;
    }
}
.ctitle {
    height: 60px;
    border-bottom: 1px solid #E1E8EE;
    padding: 20px 10px;
    color: #5E6977;
    font-size: 18px;
    font-weight: 400;
}
.cbtn {
    width: 30px;
    height: 30px;
    background-color: #E1E8EE;
    border-radius: 6px;
    border: none;
    cursor: pointer;
}
.ccbox{
  margin: auto auto;
  display: contents;
}
</style>
