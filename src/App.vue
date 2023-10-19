<script>
import themes from "./themes.json";
import Svg from './Svg.vue'
import Icon from './icon.vue'

export default {
  data() {
    return {
      themes,
      theme: themes[0],
    };
  },
  methods: {
    handleTheme(type) {
      // find the theme in themes variable
      var filtered = themes.filter(function (item) {
        return item.type === type;
      });

      // get the actual existing theme
      if (filtered.length >= 1) {
        this.theme = filtered[0];
      } else {
        this.theme = themes[0];
      }
      // do stuff on this website
      document.documentElement.className = this.theme.plate;

      // save to user's setting
      // localStorage.setItem("theme", this.theme.type)
    },
  },
  mounted() {
    // get the user's setting
    this.handleTheme(/*localStorage.getItem("theme")*/);
  },
};
</script>

<template>
  <div class="sm:p-12 min-h-screen" :class="theme.plate">
    <div
      class="mx-auto mb-4 flex flex-wrap gap-2 justify-center rounded-md border p-4"
      style="max-width: 640px"
    >
      <div class="text-center">
        <Icon></Icon>
      </div>
      <div class="grow text-right">
        <h1 class="mb-2 text-3xl font-medium xl:text-4xl">Theme Universe</h1>
        <a class="inline-block rounded-md border px-3 py-1.5" :class="theme.button" href="https://zummon.page/" target="_blank"> Made by zummon </a>
      </div>
    </div>
    <div class="mx-auto" style="max-width: 768px;" :class="theme.svgcolor">
      <Svg></Svg>
    </div>
    <div class="rounded-md p-4 mx-auto" style="max-width: 640px;" :class="theme.card">
      <div class="flex flex-wrap gap-2">
        <div class="grow">
          <h1 class="mb-2 text-3xl font-medium xl:text-4xl">How does it work?</h1>
          <h4 class="text-lg font-medium xl:text-xl">Select one of the options to see</h4>
        </div>
        <div class="">
          <select
            class="rounded-md text-black text-lg"
            :size="themes.length"
            :value="theme.type"
            @change="handleTheme($event.currentTarget.value)"
          >
            <option
              v-for="item in themes"
              :value="item.type"
              :key="item.type"
            >
              {{ item.name }}
            </option>
          </select>
        </div>
      </div>
      <p class="mt-2">
        Lorem ipsum dolor sit amet consectetur adipisicing elit.
        Repellendus tempora possimus ullam tenetur atque temporibus,
        praesentium pariatur quibusdam sunt voluptate quaerat repellat,
        suscipit cum assumenda ea reiciendis accusantium debitis expedita!
      </p>
    </div>
  </div>
</template>
