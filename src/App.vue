<template>
  <div
    class="bg-gray-900 text-gray-100 py-3.5 px-6 shadow md:flex justify-between item-center"
  >
    <div class="flex items-center cursor-pointer">
      <span class="text-green-500 text-xl mr-1">
        <i class="bi bi-messenger"></i>
      </span>
      <h1 class="text-xl">Designer</h1>
    </div>

    <span
      @click="MenuOpen()"
      class="right-10 absolute md:hiddenright-6 top-1.5 cursor-pointer text-4xl"
      v-if="isMobileView"
    >
      <i :class="[open ? 'bi bi-x' : 'bi bi-filter-left']"></i>
    </span>

    <ul
      class="md:flex md:items-center md:px-0 px-6 md:pb-0 pb-10 md:static absolute bg-gray-900 md:w-auto w-full top-14 durationn-700 ease-in"
      :class="[open ? 'left-0' : 'left-[-100%]']"
    >
      <li class="md:mx-4 md:my-0 my-6" v-for="link in Links">
        <a :href="link.link" class="text-xl hover:text-green-500">{{
          link.name
        }}</a>
      </li>

      <Button>Get Started</Button>
    </ul>
  </div>
</template>

<style scoped></style>

<script>
import { ref } from "vue";
import Button from "./components/GetStarted.vue";
export default {
  components: {
    Button,
  },
  data() {
    return {
      isMobileView: false,
    };
  },
  mounted() {
    // Check the screen width on component mount and whenever the window is resized
    window.addEventListener("resize", this.checkMobileView);
    this.checkMobileView();
  },
  methods: {
    // Adjust the breakpoint as per your needs
    checkMobileView() {
      this.isMobileView = window.innerWidth <= 768;
    },
    beforeDestroy() {
      // Remove the event listener when the component is destroyed
      window.removeEventListener("resize", this.checkMobileView);
    },
  },
  setup() {
    let open = ref(false);
    let Links = [
      { name: "Home", link: "#" },
      { name: "Services", link: "#" },
      { name: "About", link: "#" },
      { name: "Blog's", link: "#" },
      { name: "Contact", link: "#" },
    ];
    function MenuOpen() {
      open.value = !open.value;
    }
    return { Links, open, MenuOpen };
  },
};
</script>
