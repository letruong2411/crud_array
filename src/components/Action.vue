<template>
  <div>
    <button @click="handleEdit">Edit</button>
    <button @click="handleRemove">Remove</button>
  </div>
</template>
<script>
const dataItem = {
  id: undefined,
  name: "",
};
export default {
  props: {
    dataItem: {
      type: Object,
      required: false,
      default: () => ({ ...dataItem }),
    },
  },
  data() {
    return {};
  },
  methods: {
    handleRemove() {
      this.$emit("handleRemove", this.dataItem);
    },
    handleEdit() {
      this.$emit("handleEdit", this.dataItem);
    },
  },
};
</script>