<template>
<section class="content">
        <table>
        <thead>
            <tr>
            <th>nom</th>
            <th>catégorie</th>
            <th>prix</th>
            <th>déscription</th>
            <th>gestion</th>
            <th>image</th>
            </tr>
        </thead>

        <tr v-for="(produit, index) in inventory" :key="index">
            <td>{{ produit.name }}</td>
            <td>{{produit.category}}</td>
            <td>{{produit.price}}</td>
            <td>{{produit.description}}</td>
            <td>
                <router-link class="modifier" :to="{name: 'product', params:{id:produit.id}}">voir</router-link>
            </td>
            <td><img :src="require(`@/assets/img/${produit.photo}`)" :alt="produit.name" /></td>
        </tr>
        </table>
</section>
</template>

<script>
export default {
  props: ['inventory', 'addTo']
}
</script>
