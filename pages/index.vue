<template>
  <div class="px-4 py-3 bg-yellow-100 h-screen">
    <nav class="px-3 py-4">
      <a class="block font-bold text-2xl text-center mb-3 md:mb-4"
        >Barcode Image Generator</a
      >
    </nav>
    <section class="mx-auto w-60 md:w-70 text-center">
      <button
        class="bg-white rounded-md py-3 px-4 border inline-block mb-3 md:mb-4"
        @click="generateRandomNumber"
      >
        Generate number: <span class="bg-red-200 rounded-md py-2 px-3">{{ number }}</span>
      </button>
      <VueBarcode
        ref="barcode"
        :value="number"
        tag="img"
        format="CODE128"
        :options="options"
        class="block mx-auto mt-3 md:mt-4"
      ></VueBarcode>
      <a
        class="inline-block bg-green-500 rounded-md text-white py-3 px-4 mt-3 md:mt-4"
        :href="link"
        download="ship label barcode"
      >
        Download Barcode
      </a>
    </section>
  </div>
</template>
<script>
import VueBarcode from "@chenfengyuan/vue-barcode";
export default {
  components: {
    VueBarcode,
  },
  data() {
    return {
      number: "111111",
      max: 100000000,
      min: 1000,
      tag: "img",
      link: "",
      options: {
        width: 2.5,
        height: 150,
      },
    };
  },
  methods: {
    generateRandomNumber() {
      this.number = Math.floor(Math.random() * (this.max - this.min + 1) + this.min);
      this.$nextTick(() => {
        this.link = this.$refs.barcode.$el.src;
      });
    },
  },
};
</script>
