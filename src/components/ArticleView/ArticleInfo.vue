<template>
  <div>
    <v-card flat>
      <v-card-text class="pl-0">
        <p v-if="price" class="display-1 font-weight-light">{{ price | priceFilter }}</p>
        <div v-else class="d-flex text-xs-left">
          <v-icon>warning</v-icon>
          <p class="headline pt-2">Sin precio</p>
        </div>
        <v-list class="pt-4">
          <v-list-tile>
            <v-list-tile-action>
              <v-icon>add_shopping_cart</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>Cantidad</v-list-tile-title>
              <v-list-tile-sub-title class="font-weight-light">{{ mlArticle.available_quantity }} disponible<template v-if="mlArticle.available_quantity > 1">s</template></v-list-tile-sub-title>
            </v-list-tile-content>
          </v-list-tile>

          <v-list-tile v-if="mlArticle.shipping && mlArticle.shipping.free_shipping">
            <v-list-tile-action>
              <v-icon>local_shipping</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>Envío gratis</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>

          <v-list-tile class="pointer">
            <v-list-tile-action>
              <v-icon>call_made</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title @click="goToMLArticle()">Ver en MercadoLibre</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>

          <v-list-tile>
            <v-list-tile-action>
              <v-icon>place</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>{{ mlSeller.address.city.charAt(0).toUpperCase() + mlSeller.address.city.substr(1) }}</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>

          <v-list-tile class="pointer">
            <v-list-tile-action>
              <v-icon>person</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>{{ mlSeller.nickname }}</v-list-tile-title>
              <v-list-tile-sub-title @click="goToSellerPage()">Ver perfil del vendedor</v-list-tile-sub-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
import { ArticlesHelper } from '../../utils'

export default {
  name: 'ArticleInfo',
  props: ['article', 'mlArticle', 'mlSeller'],
  computed: {
    price () {
      return ArticlesHelper.price(this.article)
    },
  },
  methods: {
    goToMLArticle () {
      window.open(this.article.permalink)
    },
    goToSeller () {
      this.$router.push(`/seller/${this.mlSeller.id}`)
    },
    goToSellerPage () {
      window.open(this.mlSeller.permalink)
    }
  },
}
</script>
