<template>
  <div>

  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { IProduct } from "../../../types/Product";

@Component({
  name: "NewProductModal",
  components: {}
})
export default class NewProductModal extends Vue {
  newProduct: IProduct = {
    createdOn: new Date(),
    updatedOn: new Date(),
    id: 0,
    description: "",
    isTaxable: false,
    isArchived: false,
    price: 0,
    name: ""
  };

  close() {
    this.$emit("close");
  }
}
</script>

<style scoped lang="scss">

</style>