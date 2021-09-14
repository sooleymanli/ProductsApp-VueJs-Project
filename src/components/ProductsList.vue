<template>
  <div>
    <h3 class="text-center" v-if="show">Məhsulların siyahısı</h3>
    <div class="row product-container pb-2">
      <div
        v-for="(item, index) in productList"
        class=" col-xs-12  col-lg-2 card m-3"
        :key="item.name"
      >
        <img
          class="card-img-top"
          :src="
            item.selectedImage == null
              ? '../src/assets/default.png'
              : item.selectedImage
          "
          :alt="item.name"
        />
        <div class="card-body ">
          <h5 class="card-title">{{ item.name }}</h5>
          <small> <strong>Ədəd : </strong> {{ item.count }} </small>
          <br />
          <small> <strong>Qiymət : </strong> {{ item.price }} </small>
          <br />

          <small> <strong>Cəm : </strong> {{ item.totalPrice }} </small>
          <button
            class="btn btn-outline-info btn-block mt-3"
            v-on:click="remove(index)"
          >
            Sil
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main";
export default {
  data() {
    return {
      productList: null,
      show: false,
    };
  },
  methods: {
    remove: function(index) {
      this.productList.splice(index, 1);
      eventBus.$emit("productAdded", this.productList);
    },
  },
  created() {
    eventBus.$on("productAdded", (data) => {
      this.productList = data;
      if (data.length > 0) {
        this.show = true;
      } else {
        this.show = false;
      }
    });
  },
};
</script>
