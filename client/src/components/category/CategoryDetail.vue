<template>
  <div>
    <h5>{{ item.Name }}</h5>
    <p>{{ item.Description }}</p>
    
    <md-subheader>PRODUCTS</md-subheader>

    <div class="row">
      <product-item v-for="item in products" :item="item" :key="item.ID" class="columns medium-4"></product-item>
    </div>
  </div>
</template>

<script>
  import axios from '../../axios-auth';
  import ProductItem from '../product/ProductItem'

  export default {
    data() {
      return {
        id: this.$route.params.id,
        item: {},
        products: []
      }
    },
    components: {
      'product-item': ProductItem
    },
    methods: {
      getCategory () {
        axios.get('/api/categories/' + this.id)
        .then((res) => {
          this.item = res.data.data;
        })
        .catch(error => window.console.log(error))
      },
      getProducts(){
        axios.get('/api/categories/' + this.id + '/products')
        .then((res) => {
          this.products = res.data.data;
        })
        .catch(error => window.console.log(error)) 
      }
    },
    mounted () {
      this.getCategory()
      this.getProducts()
    }
  }
</script>