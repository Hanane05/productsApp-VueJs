<template>
<form class="add-form" @submit.prevent="updateProduct">
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

  <button class="btn">mettre à jour produit</button>
  <button class="supprimer" @click="deleteProduct">supprimer</button>
  </form>
</template>

<script>
import ProductDataService from '@/services/ProductDataService'
export default {
  props: ['inventory', 'removeInv', 'remItem', 'updateInv'],
  data () {
    return {
      message: null,
      submitted: false,
      product: {},
      id: parseInt(this.$route.params.id)
    }
  },
  methods: {
    updateProduct () {
      ProductDataService.update(this.id, this.product)
        .then(response => {
          this.updateInv(this.productIndex, this.product)
          this.$router.push({ name: 'product', params: { id: this.id } })
        })
    },
    deleteProduct () {
      ProductDataService.delete(this.id)
        .then(response => {
          this.removeInv(this.productIndex)
          this.$router.push({ name: 'products' })
        })
    }
  },
  computed: {
    productIndex () {
      const index = this.inventory.findIndex((p) => {
        return p.id === this.id
      })
      return index
    }
  },
  mounted () {
    ProductDataService.get(this.id)
      .then(response => {
        this.product = response.data
      })
  }
}
</script>
