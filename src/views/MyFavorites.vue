<template>
  <v-container class="favorites">
    <div class="d-flex align-center justify-space-between mt-2 mb-4">
      <h2 class="blue-grey--text text--lighten-5">My Favorites</h2>
      <transition name="fade">
        <v-btn
          v-if="$store.getters.getFavorites.length"
          @click="dialog = true"
          color="orange darken-4"
          text
        >
          Clear Favorites
        </v-btn>
      </transition>
    </div>

    <transition name="fade" mode="out-in">
      <v-row v-if="$store.getters.getFavorites.length" :key="1">
        <v-col
          v-for="(item, i) in $store.getters.getFavorites"
          :key="i"
          cols="12"
          sm="6"
          lg="4"
          class="picture-container pb-2"
        >
          <v-btn icon @click="$store.commit('removeFromFavorites', item)">
            <v-icon color="red">mdi-heart-off</v-icon>
          </v-btn>
          <img :src="item.url" alt="" />
        </v-col>
      </v-row>

      <div v-else :key="2" class="d-flex flex-column align-center mt-15 pt-10">
        <img src="@/assets/pictures.png" class="placeholder-picture" alt="" />
        <!-- The image above is made by www.freepik.com from https://www.flaticon.com/ -->
        <small class="mt-2 blue-grey--text text--lighten-5">
          No pictures in your favorites for now...
        </small>
      </div>
    </transition>

    <v-dialog v-model="dialog" max-width="400px">
      <ClearFavoritesDialog @close="dialog = false" @confirm="$store.commit('clearFavorites')" />
    </v-dialog>
  </v-container>
</template>

<script>
import ClearFavoritesDialog from "@/components/ClearFavoritesDialog.vue";

export default {
  name: "MyFavorites",
  data() {
    return {
      dialog: false,
    };
  },
  components: { ClearFavoritesDialog },
  async created() {
    this.$store.commit("retrieveFavoritesFromLocalStorage");
  },
};
</script>

<style lang="scss" scoped>
.favorites {
  .picture-container {
    position: relative;

    > button {
      position: absolute;
      right: 18px;
      top: 18px;
    }

    img {
      width: 100%;
      border: 1px solid #415355;
      border-radius: 4px;
    }
  }
}
</style>
