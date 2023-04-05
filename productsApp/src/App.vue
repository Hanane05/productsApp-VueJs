<template>
<header class="header">
    <h1>Produits</h1>
    <router-link to="/">Accueil</router-link>
    <router-link to="/products">Produits</router-link>
    <router-link class="nav-link" to="/new-product">Nouveau Produit</router-link>
</header>

<Router-view
:inventory = "inventory"
:addTo = "addToCart"
:addInv = "addInventory"
:removeInv = "removeInventory"
:remItem = "removeItem"
:updateInv = "updateInventory"
/>
</template>

<script>
import ProductDataService from '@/services/ProductDataService'

export default {
  components: {
  },
  data: () => {
    return {
      showSideBar: false,
      inventory: [],
      cart: {}
    }
  },
  methods: {
    addInventory (product) {
      this.inventory.push(product)
    },
    removeInventory (index) {
      this.inventory.splice(index, 1)
    },
    updateInventory (index, data) {
      this.inventory[index].name = data.name
      this.inventory[index].photo = data.photo
      this.inventory[index].price = data.price
      this.inventory[index].description = data.description
      this.inventory[index].type = data.type
    }
  },
  mounted () {
    ProductDataService.getAll()
      .then(response => {
        this.inventory = response.data
      })
  }
}
</script>
