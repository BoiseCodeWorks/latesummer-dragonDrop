<template>
  <div class="Rooms col-6" dropzone="zone" @dragover.prevent @drop.prevent="moveItem()">
    {{roomData.name}}
    <div class="row space-evenly mt-3">
      <items
        v-for="(item,index) in items"
        :itemData="item"
        :key="item.id"
        :roomId="roomData.id"
        draggable="true"
        @dragstart="reorderItem(item, index)"
      />
    </div>
  </div>
</template>


<script>
import Items from "../components/Item";
export default {
  name: "rooms",
  props: ["roomData"],
  data() {
    return {};
  },
  methods: {
    //for first way
    reorderItem(item, index) {
      // console.log(item, index);
      this.$store.dispatch("setItemToMove", {
        item: item,
        oldRoom: this.roomData,
      });
    },
    moveItem() {
      //for first way
      // let moveData = {
      //   newRoomId: this.roomData.id,
      //   oldRoomId: this.tempItem.oldRoom.id,
      //   itemToMove: this.tempItem.item,
      // };

      let item = JSON.parse(event.dataTransfer.getData("data"));
      let moveData = {
        oldRoomId: event.dataTransfer.getData("room"),
        itemToMove: item,
        newRoomId: this.roomData.id,
      };
      // console.log(moveData);
      this.$store.dispatch("moveItem", moveData);
    },
  },
  computed: {
    items() {
      return this.roomData.items;
    },

    //for first way
    // tempItem() {
    //   return this.$store.state.tempItem;
    // },
  },
  components: {
    Items,
  },
};
</script>


<style scoped>
.Rooms {
  height: 30vh;
  background-color: white;
  border: 1px;
  border-style: solid;
  border-color: black;
}
</style>