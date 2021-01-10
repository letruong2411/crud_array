<template>
  <div id="app">
    <form method="POST" @submit.prevent="onSubmit">
      <input
        v-model="formData.name"
        type="text"
        placeholder="Please input note"
      />
      <button>Submit</button>
    </form>
    <ul>
      <li v-for="item in list" :key="item.id">
        <span>{{ item.name }}</span>
        <action
          @handleRemove="onRemove"
          :dataItem="item"
          @handleEdit="onEdit"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import Action from "@/components/Action.vue";
const formDefault = {
  id: undefined,
  name: "",
};
export default {
  name: "App",
  components: {
    Action,
  },
  data() {
    return {
      formData: { ...formDefault },
      mode: "ADD",
      list: [
        {
          id: 1,
          name: "Note 1",
        },
        {
          id: 2,
          name: "Note 2",
        },
        {
          id: 3,
          name: "Note 3",
        },
        {
          id: 4,
          name: "Note 4",
        },
      ],
    };
  },
  methods: {
    onSubmit() {
      if (this.formData.name.length > 0 && this.mode === "ADD") {
        this.list.push({
          id: Math.round(Math.random() * 10000),
          name: this.formData.name,
        });
        this.formData = { ...formDefault };
      } else if (this.formData.name.length > 0 && this.mode === "EDIT") {
        const index = this.list.findIndex(
          (item) => item.id === this.formData.id
        );
        this.list[index] = { ...this.formData };
        this.mode = "ADD";
        this.formData = { ...formDefault };
      } else return;
    },
    onRemove(dataItem) {
      // console.log(dataItem);
      const index = this.list.findIndex((item) => item === dataItem);
      this.list.splice(index, 1);
    },
    onEdit(dataItem) {
      console.log(dataItem);
      this.mode = "EDIT";
      this.formData = { ...dataItem };
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

ul {
  width: 300px;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
}

input {
  margin-right: 4px;
}

button + button {
  margin-left: 4px;
}
</style>
