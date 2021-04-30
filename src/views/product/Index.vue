<template>
  <div>
      <div id="page-wrap">
          <div class="grid-wrap">
            <ProductItem 
              v-for="(product, index) in products"
              :key="index"

              :product="product"
            />
          </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
// import { products } from '../../data-seed'
import ProductItem from '../../components/ProductItem'

export default {
  components: {
    ProductItem
  },
  data() {
      return {
          products: []
      }
  },
  async created() {
    const result = await axios.get('http://localhost:8000/api/products')
    this.products = result.data
  }
}
</script>

<style scoped>
  .grid-wrap {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin-top: 16px;
  }
</style>