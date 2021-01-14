<template>
  <div  v-if="computerChoice.length">
    <div :class="computerChoice" class="btn-chosen"></div>
  </div>
  <div v-else>
    Sheldon is watching you!
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const Sheldon = defineComponent({
  props: {
    computerChoice: String,
  },
});

export default Sheldon;
</script>
