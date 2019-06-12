<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <counter />
    <ItemList />
  </div>
</template>

<script>
import Counter from "./Counter.vue";
import ItemList from "./ItemList.vue";

export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  components: {
    Counter,
    ItemList
  }
};
</script>
