<template>

  <article v-if="product" class="product">
    <div>
      <div>Code: {{ product.id }}</div>
      <div>Catégorie: {{ product.category }}</div>
      <h1>Nom: {{ product.name }}</h1>
      <div>Prix: {{ product.price }}</div>
      <div>Description: {{ product.name }}</div>
      <router-link class="modifier" :to="{name: 'edit-product', params:{id:product.id}}">modifier</router-link>
    </div>
    <img class="" :src="require(`@/assets/img/${product.photo}`)" :alt="product.name" />
    </article>

</template>

<script>
export default {
  props: ['inventory', 'addTo'],
  data () {
    return {
      id: parseInt(this.$route.params.id)
    }
  },
  computed: {
    product () {
      const product = this.inventory.find((p) => {
        return p.id === this.id
      })
      return product
    }
  }
}
</script>
