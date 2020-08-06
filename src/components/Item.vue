<template>
  <div class="item col-1" @dragstart="moveItem()">
    <img :src="itemData.url" alt="img" />
  </div>
</template>


<script>
export default {
  name: "item",
  props: ["itemData", "roomId"],
  data() {
    return {};
  },
  computed: {},
  methods: {
    moveItem() {
      //emit to parent first way
      // this.$emit("dragstart");

      //use events to set data for 2nd way
      event.dataTransfer.setData("data", JSON.stringify(this.itemData));
      event.dataTransfer.setData("room", this.roomId);
    },
  },
  components: {},
};
</script>


<style scoped>
img {
  height: 5vh;
  width: 4vw;
  background-color: white;
  border: 1px;
  border-style: solid;
  border-color: black;
}
</style>