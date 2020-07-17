<template>
  <div class="product">
    <HeaderShayna />
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text text-left product-more">
              <router-link to="/">
                <i class="fa fa-home"></i> Home
              </router-link>
              <span>Detail</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="gambar_default" alt />
                </div>
                <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                  <carousel :nav="false" :dots="false" class="product-thumbs-track ps-slider">
                    <div
                      v-for="barang in productDetails.galleries"
                      :key="barang.id"
                      class="pt"
                      @click="changeImage(barang.photo)"
                      :class="barang.photo == gambar_default ? 'active' : ''"
                    >
                      <img :src="barang.photo" alt />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details text-justify">
                  <div class="pd-title">
                    <span>{{productDetails.type}}</span>
                    <h3>{{productDetails.name}}</h3>
                  </div>
                  <div class="pd-desc">
                    <p v-html="productDetails.description"></p>
                    <h4>${{productDetails.price}}</h4>
                  </div>
                  <div class="quantity">
                    <a
                      @click="saveKeranjang(productDetails.id)"
                      href="#"
                      class="primary-btn pd-cart"
                    >Add To Cart</a>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->
    <RelatedShayna />
    <Footer />
  </div>
</template>

<script>
import RelatedShayna from "../components/RelatedShayna";
import Footer from "@/components/Footer.vue";
import HeaderShayna from "@/components/HeaderShayna.vue";
import carousel from "vue-owl-carousel";
import axios from "axios";
export default {
  name: "product",
  components: {
    HeaderShayna,
    Footer,
    carousel,
    RelatedShayna
  },
  data() {
    return {
      gambar_default: "",
      productDetails: [],
      keranjanguser: []
    };
  },
  methods: {
    changeImage(urlImage) {
      this.gambar_default = urlImage;
    },
    setDataPicture(data) {
      // get object productDetails dengan data dari APi
      this.productDetails = data;
      // get gambar default dari API
      this.gambar_default = data.galleries[0].photo;
    },
    saveKeranjang(idProduct) {
      this.keranjangUser.push(idProduct);
      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem("keranjangUser", parsed);
    }
  },
  mounted() {
    if (localStorage.getItem("keranjangUser")) {
      try {
        this.keranjangUser = JSON.parse(localStorage.getItem("keranjangUser"));
      } catch (e) {
        localStorage.removeItem("keranjangUser");
      }
    }
    axios
      .get("http://shayna-backend.belajarkoding.com/api/products", {
        params: {
          id: this.$route.params.id
        }
      })
      .then(res => this.setDataPicture(res.data.data))
      .catch(err => console.log(err));
  }
};
</script>

<style >
.product-thumbs .pt {
  margin-right: 10px;
}
</style>