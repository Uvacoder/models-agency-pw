<template>
  <div>
    <ul class="flex flex-row md:flex-col">
      <li v-for="color of colors" :key="color">
        <component
          :is="`icon-${color}`"
          :class="getClasses(color)"
          @click="$colorMode.preference = color"
        />
      </li>
    </ul>
    <!-- <p>
      <ColorScheme placeholder="..." tag="span">
        Color mode: <b>{{ $colorMode.preference }}</b>
        <span v-if="$colorMode.preference === 'system'">(<i>{{ $colorMode.value }}</i> mode detected)</span>
      </ColorScheme>
    </p> -->
  </div>
</template>

<script>
import IconLight from "@/assets/icons/light.svg?inline";
import IconDark from "@/assets/icons/dark.svg?inline";
import IconSepia from "@/assets/icons/sepia.svg?inline";

export default {
  components: {
    IconLight,
    IconDark,
    IconSepia,
  },
  data() {
    return {
      colors: ["light", "dark", "sepia"],
    };
  },
  methods: {
    getClasses(color) {
      /*
      Does not set classes on ssr preference is system (because we know them on client-side)
      Не устанавливает классы для ssr, предпочтение является системным (потому что мы знаем их на стороне клиента)
      */
      if (this.$colorMode.unknown) {
        return {};
      }
      return {
        preferred: color === this.$colorMode.preference,
        selected: color === this.$colorMode.value,
      };
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
ul li {
  padding: 5px;
}
p {
  margin: 0;
  padding-top: 5px;
  padding-bottom: 20px;
}
.feather {
  position: relative;
  top: 0px;
  cursor: pointer;
  padding: 7px;
  background-color: var(--bg-secondary);
  border: 2px solid var(--border-color);
  margin: 0;
  border-radius: 5px;
  transition: all 0.1s ease;
  width: 42px;
}
.feather:hover {
  left: -3px;
}
.feather.preferred {
  border-color: var(--color-primary);
  left: -3px;
}
.feather.selected {
  color: var(--color-primary);
}
</style>
