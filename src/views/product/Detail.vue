<template>
  <div>
      <div id="page-wrap" v-if="product">
        <div id="img-wrap">
          <img :src="`http://localhost:8000${product.imageUrl}`" alt="">
        </div>
        <div id="product-details">
          <h1>{{ product.name }}</h1>
          <h3 id="price">Rp{{ product.price }}</h3>
          <p>Average rating: {{ product.averageRating }}</p>
          <button id="add-to-cart">Add to Cart</button>
          <p>{{ product.description }}</p>
        </div>
      </div>

      <NotFound v-else/>
  </div>
</template>

<script>
import axios from 'axios'
// import { products } from '../../data-seed'
import NotFound from '../errors/404'

export default {
  components: {
    NotFound
  },
  data() {
    return {
      product: {}
    }
  },
  async created() {
    const code = this.$route.params.id
    const result = await axios.get(`http://localhost:8000/api/products/${code}`)
    this.product = result.data
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