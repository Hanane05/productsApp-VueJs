<template>
<form class="add-form" @submit.prevent="saveProduct">
  <div class="form-control">
      <label>Nom produit</label>
      <input
      type='text'
      placeholder="ajouter produit"
      v-model="product.name"
      />
  </div>

  <div class="form-control">
      <label>Prix</label>
      <input
      type='number'
      placeholder="Prix de produit"
      v-model="product.price"
      min="0"
      />
  </div>

  <div class="form-control">
      <label>Description</label>
      <textarea rows="4"
      placeholder="Description de produit"
      v-model="product.description"
      ></textarea>
  </div>

  <div class="form-control">
      <label>Catégorie</label>
      <select v-model="product.category">
      <option value="" selected disabled></option>
      <option value="furniture">furniture</option>
      <option value="electronics">electronics</option>
      <option value="Home appliance">Home appliance</option>
      </select>
  </div>

  <div class="form-control">
      <label>Image de produit</label>
      <input
      type='text'
      placeholder="ajouter produit"
      v-model="product.photo"
      />
  </div>

  <button class="btn">ajouter produit</button>
  </form>

  </template>

<script>
import ProductDataService from '@/services/ProductDataService'
export default {
  props: ['addInv'],
  data () {
    return {
      message: null,
      submitted: false,
      product: {
        name: '',
        photo: '',
        price: '',
        description: '',
        category: ''
      }
    }
  },
  methods: {
    saveProduct () {
      ProductDataService.create(this.product)
        .then(response => {
          this.product.id = response.data.id
          this.addInv(this.product)
          this.message = null
          this.submitted = true
          this.$router.push({ name: 'products' })
        })
        .catch(e => {
          this.message = e.response.data.message
        })
    },
    newProduct () {
      this.submitted = false
      this.product = {}
    }
  }
}
</script>
