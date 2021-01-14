<template>
  <div class="btn-fight center-xs middle-xs">
    <div v-if="result">
      {{result}}
      Choose weapon again.
    </div>
    <div v-else-if="fighting" class="extras">
      fighting...
    </div>
    <div v-else-if="yourChoice" @click="$emit('attacking')">
      <div class="extras">
        ATTACK
        </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const Fight = defineComponent({
  props: {
    result: String,
    fighting: Boolean,
    yourChoice: String,
  },
});

export default Fight;
</script>
