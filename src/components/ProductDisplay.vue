<template>
    <div
      class="product-container"
      :class="
        // Set background color based on product availability
        !ProductAvailable
          ? 'bg-gray'
          : products.data.category === 'men\'s clothing'
          ? 'bg-lightBlue'
          : 'bg-lightPurple'
      "
    >
      <!-- Loading Indicator -->
      <div v-if="loading">
        <SkeletonLoader />
      </div>
      <div class="product-show">
        <!-- Not Available Product -->
        <div
          class="product-not-available"
          :class="ProductAvailable ? 'display-none' : 'product-not-available'"
        >
          <!-- Information and Button for Not Available Product -->
          <p class="txt-not">This product is unavailable to show</p>
          <button class="btn-not-available" @click="nextProduct()">
            Next product
          </button>
        </div>
  
        <!-- Available Product -->
        <div
          class="product-available"
          :class="!ProductAvailable ? 'display-none' : 'product-available'"
        >
          <!-- Left Section - Product Image -->
          <div class="product-left-image">
            <img :src="products?.data?.image" class="product-img" />
          </div>
  
          <!-- Right Section - Product Details -->
          <div class="product-right-details">
            <!-- Product Title -->
            <h1
              class="product-title"
              :class="
                products?.data?.category === 'men\'s clothing'
                  ? 'color-navyBlue'
                  : 'color-magentaPurple'
              "
            >
              {{ products?.data?.title }}
            </h1>
  
            <!-- Product Information Category and Rating -->
            <div class="product-info">
              <!-- Product Category -->
              <p>{{ products?.data?.category }}</p>
              <div class="product-rate">
                <!-- Product Rating -->
                <p class="product-rating">
                  {{ products?.data?.rating?.rate }} / 5
                </p>
                <!-- Rating Circles -->
                <div class="product-rating-circle">
                  <div class="full-circle"></div>
                  <div class="full-circle"></div>
                  <div class="full-circle"></div>
                  <div class="not-full-circle"></div>
                  <div class="not-full-circle"></div>
                </div>
              </div>
            </div>
            <hr />
  
            <!-- Product Description -->
            <p class="product-desc">{{ products?.data?.description }}</p>
  
            <!-- Product Price and Buttons -->
            <div class="bottom">
              <hr />
              <!-- Product Price -->
              <h2
                class="product-price"
                :class="
                  products?.data?.category === 'men\'s clothing'
                    ? 'color-navyBlue'
                    : 'color-magentaPurple'
                "
              >
                ${{ products?.data?.price }}
              </h2>
  
              <!-- Buy and Next Product Buttons -->
              <div class="btn-container">
                <button
                  class="btn"
                  :class="
                    products?.data?.category === 'men\'s clothing'
                      ? 'color-white bg-navyBlue'
                      : 'color-white bg-magentaPurple'
                  "
                >
                  Buy Now
                </button>
                <button
                  @click="nextProduct()"
                  class="btn btn-next"
                  :class="
                    products?.data?.category === 'men\'s clothing'
                      ? 'border-navyBlue'
                      : 'border-magentaPurple'
                  "
                >
                  Next Product
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import SkeletonLoader from "../components/SkeletonLoader.vue";
  
  export default {
    name: "EcommerceProduct",
    components: {
      SkeletonLoader,
    },
  
    data() {
      return {
        index: 0,
        products: {},
        loading: false,
        ProductAvailable: false,
      };
    },
  
    methods: {
      // Function to fetch data from API
      async GetAPI() {
        try {
          const url = `https://fakestoreapi.com/products/${this.index}`;
          const response = await fetch(url);
  
          // Handle network errors
          if (!response.ok) {
            throw new Error("Request Failed");
          }
  
          // Parse JSON response
          const result = await response.json();
          return result;
        } catch (error) {
          // Handle error messages
          this.error = error.message;
        }
      },
  
      // Function to fetch and display the next product
      async nextProduct() {
        this.loading = true;
  
        // Increment index or reset to 1
        if (this.index !== 20) {
          this.index++;
        } else {
          this.index = 1;
        }
  
        // Fetch data from API
        const data = await this.GetAPI();
  
        // Check if the product category is valid
        if (
          data.category === "men's clothing" ||
          data.category === "women's clothing"
        ) {
          this.products = { data };
          this.ProductAvailable = true;
        } else {
          this.ProductAvailable = false;
        }
  
        this.loading = false;
      },
    },
  
    mounted() {
      this.nextProduct();
    },
  };
  </script>
  
  <style>
  @import url("../assets/style/store.css");
  </style>
  