<template>
  <div class="inventory-container">
    <h1 id="inventoryTitle">
      Inventory Dashboard
    </h1>
    <hr />
    <br />
    <div class="inventory-actions">
      <solar-button
          @click.native="showNewProductModal"
                    id="addNewBtn">Add New Item
      </solar-button>

     <solar-button @click.native="showShipmentModal" id="receiveShipmentBtn">
       Receive Shipment
     </solar-button>
   </div>

    <table id="inventoryTable" class="table">
      <tr>
        <th>Item</th>
        <th>Quantity On Hand</th>
        <th>Unit Price</th>
        <th>Taxable</th>
        <th>Delete</th>
      </tr>
      <tr v-for="item in inventory" :key="item.id">
        <td>
          {{item.product.name}}
        </td>
        <td>
          {{item.quantityOnHand}}
        </td>
        <td>
          {{item.product.price | price}}
        </td>
        <td>
          <span v-if="item.product.isTaxable">
            Yes
          </span>
          <span v-else>
            No
          </span>
        </td>
        <td>
          <div>
            x
          </div>
        </td>
      </tr>
    </table>
    <new-product-modal v-if="isNewProductVisible" @close="closeModals"/>
    <shipment-modal v-if="isShipmentVisible" :inventory="inventory" @close="closeModals"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import { IProductInventory } from "../../types/Product";
import SolarButton from "@/components/SolarButton.vue";

@Component({
  name: "Inventory",
  components: { SolarButton }
})
export default class Inventory extends Vue {

  isNewProductVisible = false;
  isShipmentVisible = false;

  inventory: IProductInventory[] = [
    {
      id: 1,
      product: {
        id: 1,
        name: "Some Product",
        description: "Good Stuff",
        price: 100,
        createdOn: new Date(),
        updatedOn: new Date(),
        isArchived: false,
        isTaxable: true
      },
      quantityOnHand: 100,
      idealQuantity: 100
    },
    {
      id: 2,
      product: {
        id: 2,
        name: "Goose Mellow",
        description: "Good Stuff",
        price: 100,
        createdOn: new Date(),
        updatedOn: new Date(),
        isArchived: false,
        isTaxable: false
      },
      quantityOnHand: 100,
      idealQuantity: 100
    },
    {
      id: 3,
      product: {
        id: 3,
        name: "Fiosa",
        description: "Good Stuff",
        price: 150,
        createdOn: new Date(),
        updatedOn: new Date(),
        isArchived: false,
        isTaxable: true
      },
      quantityOnHand: 50,
      idealQuantity: 30
    }
  ];

  showShipmentModal(){
    console.log("Hello, World");
  }

  showNewProductModal(){
    console.log("Hello, World");
  }

  closeModals() {
    this.isShipmentVisible = false;
    this.isNewProductVisible = false;
  }

}
</script>

<style scoped lang="scss">

</style>