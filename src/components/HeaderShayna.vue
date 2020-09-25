<template>
  <!-- Header Section Begin -->
  <header class="header-section">
    <div class="header-top">
      <div class="container">
        <div class="ht-left">
          <div class="mail-service">
            <i class="fa fa-envelope"></i>
            izmi.store@gmail.com
          </div>
          <div class="phone-service">
            <i class="fa fa-phone"></i>
            +62 895.3349.29462
          </div>
        </div>
        <div class="ht-right">
          <a href="login.html" class="login-panel"
            ><i class="fa fa-user"></i>Masuk</a
          >
        </div>
      </div>
    </div>
    <div class="container">
      <div class="inner-header">
        <div class="row">
          <div class="col-lg-2 col-md-2">
            <div class="logo">
              <a href="/">
                <img src="img/logo_ok.png" alt="" />
              </a>
            </div>
          </div>
          <div class="col-lg-7 col-md-7"></div>
          <div class="col-lg-3 text-right col-md-3">
            <ul class="nav-right">
              <li class="cart-icon">
                Keranjang Belanja &nbsp;
                <a href="#">
                  <i class="icon_bag_alt"></i>
                  <span>{{ keranjangUser.length }}</span>
                </a>
                <div class="cart-hover">
                  <div class="select-items">
                    <table>
                      <tbody v-if="keranjangUser.length > 0">
                        <tr
                          v-for="keranjang in keranjangUser"
                          :key="keranjang.id"
                        >
                          <td class="si-pic">
                            <img
                              class="photo-item "
                              :src="keranjang.photo"
                              alt=""
                            />
                          </td>
                          <td class="si-text">
                            <div class="product-selected">
                              <p>${{ keranjang.price }} x 1</p>
                              <h6>{{ keranjang.name }}</h6>
                            </div>
                          </td>
                          <td
                            @click="removeItem(keranjang.id)"
                            class="si-close"
                          >
                            <i class="ti-close"></i>
                          </td>
                        </tr>
                      </tbody>
                      <tbody v-else>
                        <tr>
                          <td>Keranjang Kosong</td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                  <div class="select-total">
                    <span>total:</span>
                    <h5>${{ totalHarga }}.00</h5>
                  </div>
                  <div class="select-button">
                    <a href="#" class="primary-btn view-card"
                      ><router-link to="/shoppingcart" style="color: #fff;"
                        >VIEW CARD
                      </router-link></a
                    >

                    <a href="#" class="primary-btn checkout-btn">CHECK OUT</a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </header>
  <!-- Header End -->
</template>

<script>
// import HeaderShayna from "@/components/HeaderShayna.vue";
// import axios from "axios";

export default {
  name: "HeaderShayna",
  data() {
    return {
      // bergungsi menyimpan atau mengambil ,ini array
      keranjangUser: [],
    };
  },
  // metod untuk menhapus keranajang belanja
  methods: {
    // idx ini sudah memiliki value atau nilai
    removeItem(idx) {
      // cari tahu id dari si item yang akan di hapus
      let keranjangUserStorage = JSON.parse(
        localStorage.getItem("keranjangUser")
      );
      // jika itemKeranjangUserStorage.id cocok dengan == idx maka
      let itemKeranjangUserStorage = keranjangUserStorage.map(
        (itemKeranjangUserStorage) => itemKeranjangUserStorage.id
      );
      // cocokan id item dengan id yang ada di storage
      let index = itemKeranjangUserStorage.findIndex((id) => id == idx);
      // jima cocok baru fungsi splice atau hapus berfungsi tergantung id nya
      this.keranjangUser.splice(index, 1);
      // 0, 1, 2, 3

      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem("keranjangUser", parsed);
      window.location.reload();
    },
  },
  mounted() {
    // jika localstorage keanjanguser tersedia
    if (localStorage.getItem("keranjangUser")) {
      try {
        // maka akan mengambil hasil array dari keranjang user
        this.keranjangUser = JSON.parse(localStorage.getItem("keranjangUser"));
      } catch (e) {
        localStorage.removeItem("keranjangUser");
      }
    }
  },
  // computed adalah fungsi untuk menghitung total yag telah di kalkulasi
  computed: {
    totalHarga() {
      return this.keranjangUser.reduce(function(items, data) {
        return items + data.price;
      }, 0);
    },
  },
};
</script>
<style scoped>
.photo-item {
  width: 80px;
  height: 80px;
}
.view-card {
  color: #fff;
}
</style>
