<template>
  <solar-modal>
    <template v-slot:header>Receive Shipment</template>
    <template v-slot:body>
      <label for="product">Product Received:</label>
      <select v-model="selectedProduct" class="shipmentItems" id="product">
        <option disabled value="">Please select one</option>
        <option v-for="item in inventory" :value="item" :key="item.product.id">
          {{ item.product.name }}
        </option>
      </select>
      <label for="qtyReceived">Quantity Received</label>
      <input type="number" id="qtyReceived" v-model="qtyReceived">
    </template>
    <template v-slot:footer>
      <solar-button type="button" @button:click="save" aria-label="Save new shipment">Save Received Shipment</solar-button>
      <solar-button type="button" @button:click="close" aria-label="Close Modal"
        >Close</solar-button
      >
    </template>
  </solar-modal>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import SolarButton from "@/components/SolarButton.vue";
import SolarModal from "@/components/modals/SolarModal.vue";
import { IProduct, IProductInventory } from "../../../types/Product";

@Component({
  name: "ShipmentModal",
  components: { SolarModal, SolarButton }
})
export default class ShipmentModal extends Vue {
  @Prop({ required: true, type: Array as () => IProductInventory[] })
  inventory!: IProductInventory[];
  selectedProduct: IProduct = {
    id: 1,
    name: "Some Product",
    description: "Good Stuff",
    price: 100,
    createdOn: new Date(),
    updatedOn: new Date(),
    isArchived: false,
    isTaxable: true
  };
  qtyReceived = 0;

  close() {
    this.$emit("close");
  }

  save() {
    this.$emit("save");
  }
}
</script>

<style scoped lang="scss"></style>
