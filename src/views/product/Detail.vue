<template>
  <div>
      <div id="page-wrap">
        <div id="img-wrap">
          <img :src="product.imageUrl" alt="">
        </div>
        <div id="product-details">
          <h1>{{ product.name }}</h1>
          <h3 id="price">Rp{{ product.price }}</h3>
          <p>Average rating: {{ product.averageRating }}</p>
          <button id="add-to-cart">Add to Cart</button>
          <p>{{ product.description }}</p>
        </div>
      </div>
  </div>
</template>

<script>
import { products } from '../../data-seed'

export default {
  data() {
    return {
      products
    }
  },
  computed: {
    product() {
      return this.products.find((p) => {
        return p.id === this.$route.params.id
      })
    }
  },
  mounted() {
    console.log(this.product)
  }
}
</script>

<style scoped>
#page-wrap {
    margin-top: 16px;
    padding: 16px;
    max-width: 600px;
  }

  #img-wrap {
    text-align: center;;
  }

  img {
    width: 400px;
  }

  #product-details {
    padding: 16px;
    position: relative;
  }

  #add-to-cart {
    width: 100%;
  }

  #price {
    position: absolute;
    top: 24px;
    right: 16px;
  }
</style>