<template>
  <div class="col-xs-6 extras">
    <div @click="$emit('chicken')">CHICKEN OUT</div>
  </div>
  <div class="col-xs-6 extras" @click="$emit('rules')">
    RULES
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const Header = defineComponent({
  props: {
  },
  emits: ['chicken', 'rules'],
});

export default Header;
</script>
