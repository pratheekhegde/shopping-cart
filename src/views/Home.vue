<template>
  <div class="famazon">
    <nav class="famazon__navbar">
      <div class="famazon__navbar-logo">
        <img src="@/assets/images/logo.png" alt="" />
      </div>
      <div class="famazon__navbar-actions">
        <ul class="list-inline m-0">
          <li class="list-inline-item">Track Order</li>
          <li class="list-inline-item">
            |
          </li>
          <li class="list-inline-item mr-0">
            <img src="@/assets/icon/search.png" alt="" />
          </li>
          <li class="list-inline-item mr-0">
            |
          </li>
          <li class="list-inline-item mr-0">
            <img src="@/assets/icon/user.png" alt="" />
          </li>
          <li class="list-inline-item mr-0">
            |
          </li>
          <li class="list-inline-item">
            <img src="@/assets/icon/shopping.png" alt="" />
          </li>
        </ul>
      </div>
    </nav>
    <section class="famazon__order-progress">
      <div class="famazon__order-progress-step step--curent">
        <div class="marker"></div>
        <div>Shopping cart</div>
      </div>
      <div class="famazon__order-progress-step step--curent">
        <div class="marker"></div>
        <div>Order Details</div>
      </div>
      <div class="famazon__order-progress-step step--curent">
        <div class="marker"></div>
        <div>Make Payment</div>
      </div>
    </section>
    <section class="famazon__ongoing-promotions">
      Shop for ${{ discount.minTotal }} or more and get
      {{ discount.discountPercentage }}% discount on your order
    </section>
    <section class="famazon__shopping-cart">
      <h4>
        Shopping Cart
      </h4>
      <shopping-cart
        :products="products"
        :pincode="pincode"
        :discount="discount"
        class="py-4"
      ></shopping-cart>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
import ShoppingCart from "@/components/ShoppingCart.vue";

export default {
  name: "home",
  components: {
    ShoppingCart
  },
  data() {
    return {
      products: [
        {
          id: 1,
          name: "Earphones",
          price: 12690,
          imageUrl: "https://via.placeholder.com/150",
          desc: "Silver"
        },
        {
          id: 2,
          tagline: "200 Cash back",
          name: "Test 6X",
          price: 14000,
          imageUrl: "https://via.placeholder.com/150",
          desc: "32GB Gold \n\n Extended Warranty",
          planLink: "http://pointstonothing.com/linktoplan",
          gift: {
            name: "Glory Selfie Stick",
            desc: "Silver Moon",
            price: 175
          }
        },
        {
          id: 3,
          name: "Test 6X",
          price: 18000,
          imageUrl: "https://via.placeholder.com/150",
          desc: "64GB Gold \n\n Extended Warranty",
          planLink: "http://pointstonothing.com/linktoplan",
          gift: {
            name: "Glory Selfie Stick",
            desc: "Silver Moon",
            price: 175
          }
        },
        {
          id: 4,
          tagline: "100 Cash back",
          name: "Earphones",
          price: 11690,
          imageUrl: "https://via.placeholder.com/150",
          desc: "White"
        },
        {
          id: 5,
          name: "Earphones",
          price: 11690,
          imageUrl: "https://via.placeholder.com/150",
          desc: "Orange"
        },
        {
          id: 6,
          name: "Test 5X",
          price: 10000,
          imageUrl: "https://via.placeholder.com/150",
          desc: "32GB Gold"
        }
      ],
      pincode: {
        "560066": {
          deliveryPrice: 50,
          cashOnDelivery: false,
          estimatedDays: {
            min: 2,
            max: 5
          }
        },
        "560067": {
          deliveryPrice: 0,
          cashOnDelivery: true,
          estimatedDays: {
            min: 3,
            max: 5
          }
        },
        "560068": {
          deliveryPrice: 0,
          cashOnDelivery: false,
          estimatedDays: {
            min: 5,
            max: 5
          }
        }
      },
      discount: {
        minTotal: 5000,
        discountPercentage: 10
      }
    };
  }
};
</script>
<style lang="scss" scoped>
.famazon {
  &__navbar {
    padding: 0.2rem 3rem;
    background: #21009d;
    display: flex;
    justify-content: space-between;
  }
  &__order-progress {
    display: flex;
    height: 100px;
    padding: 20px;
    background: #fff;
    box-shadow: 0 1px 4px rgba(11, 37, 69, 0.1);
    justify-content: center;
    align-items: center;
  }
  &__ongoing-promotions {
    margin: 1.5rem 5rem;
    display: flex;
    color: #fff;
    padding: 5px;
    justify-content: center;
    background: #8386ca;
  }
  &__order-progress-step {
    .step--active {
    }
  }
  &__navbar-logo {
    display: flex;
    align-items: center;
  }
  &__navbar-actions {
    font-size: 11px;
    color: #fff;
    display: flex;
  }
  &__shopping-cart {
    padding: 1rem 5rem;
  }
}
</style>
