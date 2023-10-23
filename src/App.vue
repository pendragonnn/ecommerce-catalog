
<template>
  <div
    :class="{
      container_cover_men: this.products[index].category === 'men\'s clothing',
      container_cover_women:
        this.products[index].category === 'women\'s clothing',
      container_not_found:
        this.products[index].category !== 'women\'s clothing' &&
        this.products[index].category !== 'men\'s clothing',
    }"
    v-if="index < 20"
  >
    <div class="container">
      <div class="container_inner_not_found" v-if="isLoading">
        <div class="loader"></div>
      </div>
      <div class="container_inner_not_found" v-else-if="this.products[index].category !== 'women\'s clothing' &&
        this.products[index].category !== 'men\'s clothing'">
        <div class="description-not-found">
          this product is unavailable to show
        </div>
        <button class="next-button-not-found" @click="nextProduct(this.products[index].id)">Next Product</button>
      </div>
      <div class="container-item" v-else>
        <div class="container-image">
          <img :src="this.products[index].image" alt="" />
        </div>
        <div class="container-description">
          <div
            :class="{
              title_men: this.products[index].category === 'men\'s clothing',
              title_women:
                this.products[index].category === 'women\'s clothing',
            }"
          >
            {{ this.products[index].title }}
          </div>
          <div class="category-rating">
            <div class="category">{{ this.products[index].category }}</div>
            <div class="rating" >
              <div class="rating_value">{{  this.products[index].rating.rate }}/5</div>
              <div class="rating_men" v-for="index in Math.floor(this.products[index].rating.rate)" :key="index"></div>
              <div class="rating_men_zero" v-for="index in 5 - Math.floor(this.products[index].rating.rate)" :key="index"></div>
            </div>
          </div>
          <div class="description-item">
            {{ this.products[index].description }}
          </div>
          <div
            :class="{
              price_men: this.products[index].category === 'men\'s clothing',
              price_women:
                this.products[index].category === 'women\'s clothing',
            }"
          >
            $ {{ this.products[index].price }}
          </div>
          <div class="button-container">
            <button
              :class="{
                buy_button_men:
                  this.products[index].category === 'men\'s clothing',
                buy_button_women:
                  this.products[index].category === 'women\'s clothing',
              }"
            >
              Buy now
            </button>
            <button
              :class="{
                next_button_men:
                  this.products[index].category === 'men\'s clothing',
                next_button_women:
                  this.products[index].category === 'women\'s clothing',
              }"
              @click="nextProduct(this.products[index].id)"
            >
              Next Product
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ProductComponentVue from "./components/ProductComponent.vue";

export default {
  data() {
    return {
      index: 0,
      products: [],
      isLoading: false,
    };
  },
  components: {
    ProductComponentVue,
  },
  methods: {
    nextProduct(id) {
      if(id === 20) {
        this.index = 1
      } else {
        this.index++
      }
      this.isLoading = true;

      setTimeout(() => {
        this.isLoading = false; 
      }, 4000);
    },
  },
  beforeCreate() {
    fetch(`https://fakestoreapi.com/products/`)
      .then((response) => response.json())
      .then((data) => {
        const filteredProducts = data.filter((product) => {
          return product.category === "men's clothing" || product.category === "women's clothing"
        })
        // const filteredId = filteredProducts.map((product) => product.id)
        // this.products = filteredProducts;
        // this.filteredId = filteredId;
        this.products = data;
      });
  },
};
</script>

<style scoped>
.active {
  background: salmon;
  border: none;
  padding: 2px;
}
</style>
