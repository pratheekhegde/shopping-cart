<template>
  <div class="cart">
    <table class="table">
      <tr>
        <th>Product</th>
        <th>Price</th>
        <th>Quantity</th>
        <th>Subtotal</th>
      </tr>
      <tr v-for="(item, idx) in cart" :key="idx">
        <td>
          <img :src="item.productImage" alt="" />
          {{ item.name }}
        </td>
        <td>
          {{ item.price + "$" }}
        </td>
        <td>
          <span
            @click="changeItemCount(item, 'decrement')"
            class="cursor-pointer"
          >
            <img src="@/assets/icon/minus.png" alt="" />
          </span>
          <input type="number" v-model.number="item.quantity" min="1" max="5" />
          <span
            @click="changeItemCount(item, 'increment')"
            class="cursor-pointer"
          >
            <img src="@/assets/icon/plus.png" alt="" />
          </span>
        </td>
        <td>
          {{ item.price * item.quantity }} $
          <span @click="removeItem(item, idx)" class="cursor-pointer">
            <img src="@/assets/icon/DELETE.png" alt="" />
          </span>
        </td>
      </tr>
    </table>

    <div class="cart__footer">
      <div class="cart__footer-left">
        <h6>Delivery Avalaiblity</h6>
        <b-form-group>
          <b-form-select
            id="exampleInput3"
            :options="pincode"
            v-model="selectedPincode"
          >
          </b-form-select>
        </b-form-group>
        <div class="d-flex"></div>
      </div>
      <div class="cart__footer-right">
        <b>Order Summary ( {{ this.cart.length }} items) </b>
        <div class="d-flex flex-column">
          <div class="d-flex justify-content-between">
            <div>Subtotal</div>
            <div>{{ subTotal }} $</div>
          </div>
          <div class="d-flex justify-content-between">
            <div>Total Discount</div>
            <div>{{ totalDiscount > 0 ? "-" : "" }} {{ totalDiscount }} $</div>
          </div>
          <div class="d-flex justify-content-between" v-if="selectedPincode">
            <div>Standard Shipping</div>
            <div>
              <span v-if="shippingCharges === 0">
                Free
              </span>
              <span v-else> {{ shippingCharges }} $ </span>
            </div>
          </div>
          <div class="d-flex justify-content-between">
            <div>Order Total</div>
            <div>
              <b>{{ totalOrder }} $</b>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["products", "discount", "pincode"],
  data() {
    return {
      config: {
        MAX_ITEM_QUANTITY: 5
      },
      selectedPincode: null,
      cart: [],
      productImages: ["Earphone.png", "phone.png", "stick.png"]
    };
  },
  computed: {
    subTotal() {
      if (this.cart.length > 0) {
        return this.cart.reduce((total, item) => {
          return total + item.quantity * item.price;
        }, 0);
      } else return 0;
    },
    totalDiscount() {
      if (this.subTotal > this.discount.minTotal) {
        return (this.discount.discountPercentage / 100) * this.subTotal;
      } else return 0;
    },
    shippingCharges() {
      if (this.selectedPincode) {
        return this.pincode[this.selectedPincode].deliveryPrice;
      } else return 0;
    },
    totalOrder() {
      return this.subTotal - this.totalDiscount + this.shippingCharges;
    }
  },
  mounted() {
    if (localStorage.getItem("cartItems")) {
      this.cart = JSON.parse(localStorage.getItem("cartItems"));
    } else this.addItemsToCart();
  },
  methods: {
    getRandomProductImage() {
      const idx = Math.floor(
        Math.random() * Math.floor(this.productImages.length)
      );
      return require(`@/assets/images/${this.productImages[idx]}`);
    },
    addItemsToCart() {
      this.cart = this.products.map(item => {
        return {
          quantity: 0,
          productImage: this.getRandomProductImage(),
          ...item
        };
      });
    },
    removeItem(item, idx) {
      this.cart.splice(idx, 1);
    },
    changeItemCount(item, type) {
      if (type === "increment") {
        if (item.quantity + 1 <= this.config["MAX_ITEM_QUANTITY"]) {
          item.quantity++;
        }
      } else {
        if (item.quantity - 1 >= 0) {
          item.quantity--;
        }
      }
    }
  },
  watch: {
    cart: {
      handler() {
        localStorage.setItem("cartItems", JSON.stringify(this.cart));
      },
      deep: true
    }
  }
};
</script>
<style lang="scss" scoped>
.cart {
  &__footer {
    padding-top: 3rem;
    display: flex;
    justify-content: space-between;
  }
  &__footer-left {
  }
  &__footer-right {
    width: 25%;
  }
}
.cursor-pointer {
  cursor: pointer;
}
</style>
