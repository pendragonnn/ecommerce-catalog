<template>
  <div
    :class="{
      container_cover_men: this.products.category === 'men\'s clothing',
      container_cover_women: this.products.category === 'women\'s clothing',
      container_not_found:
        this.products.category !== 'women\'s clothing' &&
        this.products.category !== 'men\'s clothing',
    }"
  >
    <div class="container">
      <div class="container_inner_not_found" v-show="isLoading">
        <div class="loader"></div>
      </div>
      <div
        class="container_inner_not_found"
        v-if="
          this.products.category !== 'women\'s clothing' &&
          this.products.category !== 'men\'s clothing'
        "
        v-show="!isLoading"
      >
        <div class="loader" v-show="isLoading"></div>
        <div class="not_found_container">
          <div class="description-not-found">
            this product is unavailable to show
          </div>
          <button
            class="next-button-not-found"
            @click="nextProduct(this.products.id)"
          >
            Next Product
          </button>
        </div>
        
      </div>
      <div class="container-item" v-else v-show="!isLoading">
        <div class="container-image">
          <img :src="this.products.image" alt="" />
        </div>
        <div class="container-description">
          <div
            :class="{
              title_men: this.products.category === 'men\'s clothing',
              title_women: this.products.category === 'women\'s clothing',
            }"
          >
            {{ this.products.title }}
          </div>
          <div class="category-rating">
            <div class="category">{{ this.products.category }}</div>
            <div class="rating">
              <div class="rating_value">{{ this.products.rating.rate }}/5</div>
              <div
                :class="{
                  rating_men: this.products.category === 'men\'s clothing',
                  rating_women: this.products.category === 'women\'s clothing',
                }"
                v-for="id in Math.round(this.products.rating.rate)"
                :key="id"
              ></div>
              <div
                :class="{
                  rating_men_zero: this.products.category === 'men\'s clothing',
                  rating_women_zero:
                    this.products.category === 'women\'s clothing',
                }"
                v-for="id in 5 - Math.round(this.products.rating.rate)"
                :key="id"
              ></div>
            </div>
          </div>
          <div class="description-item">
            {{ this.products.description }}
          </div>
          <div
            :class="{
              price_men: this.products.category === 'men\'s clothing',
              price_women: this.products.category === 'women\'s clothing',
            }"
          >
            $ {{ this.products.price }}
          </div>
          <div class="button-container">
            <button
              :class="{
                buy_button_men: this.products.category === 'men\'s clothing',
                buy_button_women:
                  this.products.category === 'women\'s clothing',
              }"
            >
              Buy now
            </button>
            <button
              :class="{
                next_button_men: this.products.category === 'men\'s clothing',
                next_button_women:
                  this.products.category === 'women\'s clothing',
              }"
              @click="nextProduct(this.products.id)"
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
export default {
  data() {
    return {
      index: 1,
      products: [],
      isLoading: false,
    };
  },
  methods: {
    nextProduct() {
      if (this.index === 20) {
        this.index = 1;
      } else {
        this.index++;
      }
      this.isLoading = true;

      setTimeout(() => {
        this.isLoading = false;
      }, 1500);

      fetch(`https://fakestoreapi.com/products/${this.index}`)
        .then((response) => response.json())
        .then((data) => {
          this.products = data;
        });
    },
  },
  created() {
    this.isLoading = true;

    setTimeout(() => {
      this.isLoading = false;
    }, 1500);
    
    fetch(`https://fakestoreapi.com/products/${this.index}`)
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
};
</script>

<style scoped>
</style>
