<template>
   <div class="container-cover">
      <div class="container">
        <div class="container-item">
          <div class="container-image">
            <img src="https://placehold.co/300x400" alt="" />
          </div>
          <div class="container-description">
            <div class="title">
              {{ filteredProduct[0].title }}
            </div>
            <div class="category-rating">
              <div class="category">woman's clothing</div>
              <div class="rating">2 ***</div>
            </div>
            <div class="description-item">
              100% POLYURETHANE(shell) 100% POLYESTER(lining) 75% POLYESTER 25%
              COTTON (SWEATER), Faux leather material for style and comfort / 2
              pockets of front, 2-For-One Hooded denim style faux leather
              jacket, Button detail on waist / Detail stitching at sides, HAND
              WASH ONLY / DO NOT BLEACH / LINE DRY / DO NOT IRON
            </div>
            <div class="price">20$</div>
            <div class="button-container">
              <button class="buy-button">Buy now</button>
              <button class="next-button">Next Product</button>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'product-component',
  props: ['filteredId', 'filteredProduct'],
  data() {
    return {

    }
  },
  mounted() {
    console.log(this.filteredProduct[0])
  }
  // mounted() {
  //   const index = 0
  //   const currentIndex = this.filteredId[index]
  //     fetch(`https://fakestoreapi.com/products/${currentIndex}`)
  //     .then((response) => response.json())
  //     .then((data) => {
  //       this.product = data
  //       console.log(data)
  //     });
  //   }
}
</script>

<style>

</style>