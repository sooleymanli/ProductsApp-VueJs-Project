<template>
<div>
  <div class="row d-flex justify-content "  >
    <div class="card  col-md-3">
      <div class="card-body tex-center d-flex align-items-center flex-column">
        <img
          height="128"
          class="img-responsive text-center mb-3"
          :src="
            product.selectedImage == null
              ? '/src/assets/default.png'
              : product.selectedImage
          "
        />
        <input
          ref="file"
          type="file"
          style="display: none;"
          @change="onChange($event)"
          class="form-control"
        />
        <button
          class="btn btn-outline-secondary "
          type="button"
          @click="$refs.file.click()"
        >
          Şəkil yüklə
        </button>
      </div>
    </div>
    <div class="col-md-5">
      <div class="col-md-11 card">
        <div class="card-body">
          <div class="form-group">
            <label>Məhsulun adı</label>
            <input
              type="text"
              class="form-control"
              placeholder="Ad daxil edin"
              v-model="product.name"
            />
          </div>
          <div class="row">
            <div class="form-group col-md-6">
              <label>Məhsulun sayı</label>
              <input
                type="text"
                class="form-control"
                placeholder="Say daxil edin"
                v-model="product.count"
              />
            </div>
            <div class="form-group col-md-6">
              <label>Məhsulun qiyməti</label>
              <input
                type="text"
                class="form-control"
                placeholder="Qiymət daxil edin"
                v-model="product.price"
              />
            </div>
          </div>
          <button class="btn btn-outline-info btn-block" @click="add">
            Əlavə et!
          </button>
        </div>
      </div>
  
    </div>
     
  </div>
     <error v-if="show" :text="errorText"></error>
       </div>

</template>

<script>
import { eventBus } from "../main";
import Error from './Error.vue';

export default {
    components: {
    Error
  },
  data() {
    return {
      product: {
        selectedImage: null,
        name: null,
        price: null,
        count: null,
        totalPrice: null,
      },
      show:false,
      productList: [],
      length:0,
      errorText:null
    };
  },
  methods: {
    onChange(e) {
      const file = e.target.files[0];
      this.product.selectedImage = URL.createObjectURL(file);
    },
    add() {

        if(this.product.name ===null || this.product.price ===null || this.product.count===null){
            this.errorText="Bütün xanaları doldurduğunuzdan əmin olun!"
this.show=true
        }else{
eventBus.$on("productAdded",data=>{
this.length=data.length
})

            if(this.length<10){
       this.show=false
   this.product.totalPrice = this.product.price * this.product.count;
      this.productList.push(this.product);
      eventBus.$emit("productAdded", this.productList);
      this.product = {
        selectedImage: null,
        name: null,
        price: null,
        count: null,
        totalPrice: null,
      };
            }else{
   this.errorText="Məhsul limitini keçmisiniz!"
this.show=true
            }
     
        }
   
    },
  },
};
</script>
