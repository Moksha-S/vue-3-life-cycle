<template>
  <main>
    <div>
      <h1>Check console</h1>
      <div ref="greeting">Hello readers !</div>
      <img ref="img" :src="img" alt="image" width="200" />
      <div>
        <button @click="demo()">Click to update</button>
        <span v-if="showText">
          comment/uncomment me to see beforeUpdate/updated hook's reactivity
        </span>
      </div>
    </div>
  </main>
</template>

<script>
//option API vue 3
export default {
  data() {
    console.log("data===== I'm data hook");
    return {
      showText: true,
      stateOfBob: "sleeping",
      img: "https://picsum.photos/seed/picsum/200/300",
    };
  },
  computed: {
    test: function () {
      return "I'm computed hook";
    },
  },
  beforeCreate() {
    console.log("beforeCreate==== I'm beforeCreate hook");
    console.log("beforeCreate==== computed hook is returning ", this.test);
  },
  created() {
    console.log("Created====  I'm created hook");
  
    console.log("Created==== Bob is currently ", this.stateOfBob);
    this.stateOfBob = "awakened but still sleeping";
    console.log("Created==== computed hook is returning ", this.stateOfBob);
  },
  beforeMount() {
    console.log("beforeMount==== beforeMountI'm beforeMount hook");
    console.log("beforeMount==== The Dom node is ", this.$refs["greeting"]);
  },
  mounted() {
    console.log("mounted==== I'm mounted hook");
    console.log("mounted==== The Dom node is ", this.$refs["greeting"]);
  },
  beforeUpdate() {
    console.log(
      "beforeUpdate==== I'm beforeUpdate hook and i can help to apply extra effects before a DOM is updated"
    );
    console.log(" beforeUpdate====  width of img div ", this.$refs.img.width);
    this.$refs.img.width = 300;
    console.log(
      " beforeUpdate====  width of img div after overriding ",
      this.$refs.img.width
    );
  },
  updated() {
    console.log("updated==== I'm updated hook");
    this.img = "https://picsum.photos/200/300"; //updates the image src
  },
  beforeUnmount() {
    console.log("beforeUnmount==== I'm beforeUnmount hook");
    // this.$refs.img.width = 0;
  },
  unmounted() {
    console.log("I'm unmounted hook");
  },

  methods: {
    demo() {
      this.showText = !this.showText;
      console.log("demo method called");
    },
  },
};
</script>
