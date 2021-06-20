<template>
  <div>
    <bounce-loader
      :loading="isLoading"
      :color="'#68d391'"
      :size="100"
    ></bounce-loader>
    <px-assets-table
      v-if="!isLoading"
      :assets="assets"
    />
  </div>
</template>

<script>
import api from '@/api.js'
import PxAssetsTable from "@/components/PxAssetsTable";

export default {
  name: "Home",
  data () {
    return {
      isLoading: false,
      assets: []
    }
  },
  components: { PxAssetsTable },
  created () {
    this.isLoading = true
    api.getAssets()
      .then((assets) => {
        this.assets = assets
      }).catch((err) => {
        console.log(err)
      })
      .finally(() => {
        this.isLoading = false
      })
  }
};
</script>