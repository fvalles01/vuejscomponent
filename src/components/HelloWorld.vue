<template>
  <di>
    <h1>Items</h1>
    <ul>
      <li v-for="item of items" :key="item.id">
        {{ item.title }}
      </li>
    </ul>
  </di>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      items: {},
      timer: "",
    };
  },
  created() {
    this.fetchData();
    this.timer = setInterval(this.fetchData, 5000);
  },
  methods: {
    async fetchData() {
      const res = await fetch("http://localhost:3001/items");
      const data = await res.json();
      this.items = data;
    },
    cancelAutoUpdate() {
      clearInterval(this.timer);
    },
  },
  beforeUnmount() {
    this.cancelAutoUpdate();
  },
};

// import axios from "axios";
// export default {
//   name: "items",
//   data() {
//     return {
//       items: [],
//       timer: "",
//     };
//   },
//   async created() {
//     try {
//       const res = await axios.get("http://localhost:3001/items");

//       this.items = res.data;
//     } catch (e) {
//       console.error(e);
//     }
//   },
// };

// export default {
//   name: "items",
//   data() {
//     return {
//       items: {},
//       timer: "",
//     };
//   },
//   created() {
//     this.fetchData();
//     this.timer = setInterval(this.fetchData, 5000);
//   },
//   methods: {
//     async fetchData() {
//       const res = await fetch("http://localhost:3001/items");
//       const items = await res.json();
//       this.answer = items;
//       console.log(items);
//     },
//     cancelAutoUpdate() {
//       clearInterval(this.timer);
//     },
//   },
//   beforeUnmount() {
//     this.cancelAutoUpdate();
//   },
// };
</script>

<style scoped>
h1 {
  text-decoration: underline;
}

li {
  color: rgb(201, 25, 25);
}
</style>
