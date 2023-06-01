<script>
import {
  ref,
  onBeforeMount,
  onMounted,
  onUpdated,
  onBeforeUpdate,
  onBeforeUnmount,
  onUnmounted,
} from "vue";
// composition API vue-3
export default {
  setup() {
    const val = ref("hello");
    console.log("setup=== Value of val is: " + val.value);

    const root = ref(null);
    onBeforeMount(() => {
      console.log("onBeforeMount==", root.value);
    });
    onMounted(() => {
      console.log("onMounted===", root.value);
    });

    const count = ref(0);
    const valUpdate = ref(0);
    onBeforeUpdate(() => {
      count.value++;
      console.log("beforeUpdate");
    });
    onUpdated(() => {
      console.log("updated() val: " + valUpdate.value);
    });

    onBeforeUnmount(() => {
      console.log("unbeforemount");
    });
    onUnmounted(() => {
      console.log("unmount");
    });
    return {
      val,
      root,
      valUpdate,
      count,
    };
  },
};
</script>

<template>
  <div class="about">
    <h1>LifeCycle composition page</h1>
    <div ref="root">Hello World</div>
    <div>
      <p>{{ valUpdate }} | edited {{ count }} times</p>
      <button @click="valUpdate = Math.random(0, 100)">Click to Change</button>
    </div>
  </div>
</template>

<style>
/* @media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
} */
</style>
