<template>
  <div class="skeleton-container">
    <div class="skeleton-show">
      <!-- Skeleton Not Available Product -->
      <div class="skeleton-not-available">
        <p class="skeleton-txt-not"></p>
        <button class="skeleton-btn-not-available"></button>
      </div>

      <!-- Available Product -->
      <div class="skeleton-available">
        <!-- Left Section - Skeleton Product Image -->
        <div class="skeleton-product-left-image">
          <div class="skeleton-img"></div>
        </div>

        <!-- Right Section - Skeleton Product Details -->
        <div class="skeleton-product-right-details">
          <h1 class="skeleton-product-title"></h1>

          <!-- Skeleton Product Information Category and Rating -->
          <div class="skeleton-product-info">
            <!-- Skeleton Product Category -->
            <p class="skeleton-product-category"></p>
            <!-- Skeleton Product Rate -->
            <div class="skeleton-product-rate"></div>
          </div>
          <hr />

          <!-- SkeletonProduct Description -->
          <p class="skeleton-product-desc">
            <span></span>
            <span></span>
            <span></span>
            <span></span>
          </p>

          <!-- Skeleton Product Price and Buttons -->
          <div class="skeleton-bottom">
            <hr />
            <!-- Skeleton Product Price -->
            <h2 class="skeleton-product-price"></h2>

            <!-- Skeleton Buy and Next Product Buttons -->
            <div class="skeleton-btn-container">
              <button class="skeleton-btn"></button>
              <button class="skeleton-btn"></button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LoaderComponent",
};
</script>

<style>
@import url("../assets/style/skeleton.css");
</style>
