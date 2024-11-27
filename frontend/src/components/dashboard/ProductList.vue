<script>
import axios from "axios";
import CreateProduct from "@/components/dashboard/CreateProduct.vue";
import UpdateProduct from "@/components/dashboard/UpdateProduct.vue";
import ShowProduct from "@/components/dashboard/ShowProduct.vue";

export default {
  components: { CreateProduct, UpdateProduct, ShowProduct },

  props: {
    userID: String,
    shopID: String,
  },

  data() {
    return {
      products: {},
      dataLoaded: false,
    };
  },

  async created() {
    try {
      // Get all products that belong to the shop.
      const shop = await axios({
        baseURL: import.meta.env.VITE_BACKENDURL,
        method: "get",
        url: "/seller/shop/show",
        params: {
          shopID: this.shopID,
          withProducts: true,
        },
      });

      this.products = shop.data.products;

      this.dataLoaded = true;
    } catch (e) {
      console.log(e);
    }
  },

  methods: {
    async deleteProduct(productID) {
      try {
        await axios({
          baseURL: import.meta.env.VITE_BACKENDURL,
          method: "delete",
          url: "/seller/product/delete",
          params: {
            productID: productID,
          },
        });

        window.location.reload();
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>

<template>
  <div class="rounded-md shadow-md w-full p-8 space-y-4">
    <div class="flex space-x-4 items-center justify-between">
      <h2 class="font-bold text-2xl flex flex-col space-y-4">Products</h2>

      <CreateProduct :shopID="this.shopID"></CreateProduct>
    </div>
    <div class="divider"></div>
    <div class="overflow-x-auto">
      <table class="table w-full">
        <!-- head -->
        <thead>
          <tr>
            <th></th>
            <th>Nom</th>
            <th>Prix</th>
            <th>Description</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr class="hover" v-for="(product, key) in this.products" :key="key">
            <td>{{ key + 1 }}</td>
            <td>{{ product.name }}</td>
            <td>{{ product.price }} €</td>
            <td class="whitespace-normal">
              {{ product.description }}
            </td>
            <td class="flex space-x-2">
              <label :for="'deleteProduct' + key" class="btn btn-error"
                >Supprimer</label
              >
              <UpdateProduct
                :product="product"
                :productKey="key"
              ></UpdateProduct>
              <ShowProduct
                :productID="product._id"
                :productKey="key"
              ></ShowProduct>
            </td>

            <input
              type="checkbox"
              :id="'deleteProduct' + key"
              class="modal-toggle"
            />
            <div class="modal">
              <div class="modal-box relative">
                <label
                  :for="'deleteProduct' + key"
                  class="btn btn-sm btn-circle absolute right-2 top-2"
                  >✕</label
                >
                <h3 class="font-bold text-lg">
                  Êtes-vous sûr de vouloir supprimer ce produit - "{{
                    product.name
                  }}"?
                </h3>
                <div class="divider"></div>
                <div class="flex space-x-4">
                  <button
                    @click="deleteProduct(product._id)"
                    class="btn btn-error btn-outline"
                  >
                    Supprimer
                  </button>
                  <label for="'deleteProduct' + key" class="btn btn-primary"
                    >Annuler</label
                  >
                </div>
              </div>
            </div>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
