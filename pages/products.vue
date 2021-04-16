<template>
    <div>
         <div class="bg-light py-3">
      <div class="container">
        <div class="row">
          <div class="col-md-12 mb-0"><a href="index.html">Home</a> <span class="mx-2 mb-0">/</span> <strong class="text-black">Shop</strong></div>
        </div>
      </div>
    </div>

    <div class="site-section">
      <div class="container">

        <div class="row mb-5">
          <div class="col-md-9 order-2">
           
           
            <div class="row mb-5">
              <!-- -->
              <div class="col-sm-6 col-lg-4 mb-4" v-for="product in products" :key="product.title">
                  <nuxt-link :to="'/product/' + product._id">
                <div class="block-4 text-center border">
                  <figure class="block-4-image" style="height: 135px;">
                  <img :src="product.image" alt="Image placeholder" class="img-fluid" style="height: 154px;">
                  </figure>
                  <div class="block-4-text p-4">
                    <p class="mb-0" style="height: 54px;">{{product.title}}</p>
                    <h5 class="font-weight-bold" style="color:#7971ea;">{{product.price}}.00 € </h5>
                  </div>
                </div>

                </nuxt-link>
              </div>
            <!-- -->


            </div>
           
          </div>

          <div class="col-md-3 order-1 mb-5 mb-md-0">
            <div class="border p-4 rounded mb-4">
              <h3 class="mb-3 h6 text-uppercase text-black d-block">Categories</h3>
              <ul class="list-unstyled mb-0">
                <li><a class="d-flex colorp" style="cursor:pointer"><span>Tous</span></a></li>
                <li v-for="category in categories" :key="category.name" class="mb-1" ><a class="d-flex colorp" style="cursor:pointer"><span>{{category.name}}</span></a></li>
              </ul>
            </div>

        
          </div>
        </div>

       
        
      </div>
    </div>
    </div>
</template>

<script>
import RangeSlider from 'vue-range-slider'
// you probably need to import built-in style
import 'vue-range-slider/dist/vue-range-slider.css'
import axios from 'axios'
export default {
data(){
  return{
      sliderValue: 100,
      products:[],
      categories:[],
      providers:[]
  }
},
components: {
  RangeSlider
},
created(){
  this.getproducts()
  this.getCategories()
  this.getProviders()
},
methods: {
   getproducts(){
     axios({
       method:'GET',
       url:'http://localhost:3030/api/v1/products'
     })
     .then(value=>{
       this.products = value.data
     })
      
   },
   getCategories(){
     axios({
       method:'GET',
       url:'http://localhost:3030/api/v1/categories'
     })
     .then(res=>{
       this.categories = res.data
     })
   },
   getProviders(){
      axios({
       method:'GET',
       url:'http://localhost:3030/api/v1/providers'
     })
     .then(res=>{
       this.providers = res.data
     })
   },
   
  
    filterProducts(type,valeur){
     this.getproducts()
      let productFilters=[]    
      switch (type) {
        case 'category':
          this.products.forEach(element => {
            if(element.category==valeur){
              productFilters.push(element)
            }
         })
          break;
        case 'color':
            this.products.forEach(element => {
            if(element.color==valeur){
              productFilters.push(element)
            }
         })
           break;
        case 'size':
          this.products.forEach(element => {
            if(element.size==valeur){
              productFilters.push(element)
            }
          })
          break;
        default:
          console.log(`Sorry, we are out of.`);
      }
     
       this.products=productFilters

    }
    
  }
};
</script>

<style scoped>

.colorp{
  color: #7971ea;
}
.slider {
  /* overwrite slider styles */
  width: 200px;
}

</style>>
