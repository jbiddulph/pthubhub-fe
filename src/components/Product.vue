<template>
  <div class="product">
    <img :src="product.image" class="product-image" />
    <div class="lower">
      <div class="text">
        <div class="title">
          {{ product ? product.title : "" }}
        </div>
        <div class="price-discounted">
          <div class="discount" v-if="discountedPrice">
            <div v-if="discountedPrice === 'FREE'">{{ discountedPrice }}</div>
            <div v-else-if="discountedPrice !== 'FREE'">
              &pound;{{ discountedPrice / 100 }}
            </div>
          </div>
          <div
            v-bind:class="[discountedPrice ? 'discounted' : '', 'price']"
            else
          >
            &pound;{{ product.price / 100 }}
          </div>
        </div>
        <div class="subtitle">
          {{ product ? product.description : "" }}
        </div>
      </div>
      <div class="avatar">
        <img :src="product.image" height="32" width="32" class="avatar" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: {
    product: {}
  },
  computed: {
    discountedPrice() {
      let discountedAmount = 0;
      let newDiscountedprice = 0;
      if (this.product.discount != null) {
        discountedAmount =
          (parseInt(this.product.discount) / 100) * this.product.price;
        newDiscountedprice = this.product.price - discountedAmount;
        if (newDiscountedprice == 0) {
          newDiscountedprice = "FREE";
        }
        return newDiscountedprice;
      } else {
        return newDiscountedprice;
      }
    }
  }
};
</script>

<style lang="scss">
@import "../assets/styles/styles.scss";
.product {
  display: flex;
  flex-direction: column;
  width: 350px;
  margin: 10px;
  border-radius: 8px;
  position: relative;
  .product-image {
    border-radius: 8px;
  }
  .lower {
    width: 90.9%;
    position: absolute;
    bottom: 0;
    font-size: 16px;
    font-weight: 600;
    padding: 16px;
    line-height: 19px;
    text-align: left;
    color: #fff;
    height: auto;
    opacity: 0.8;
    border-radius: 0px 0px 8px 8px;
    display: flex;
    justify-content: space-between;
    .text {
      .price-discounted {
        display: flex;
        .discount {
          margin-right: 20px;
        }
        .discounted {
          color: $lightgrey;
          text-decoration: line-through;
        }
      }
    }
    .subtitle {
      color: $lightgrey;
      font-size: 12px;
      line-height: 14px;
    }
    .avatar {
      border-radius: 16px;
    }
  }
}
</style>
