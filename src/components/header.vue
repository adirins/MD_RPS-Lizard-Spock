<template>
  <div class="row header center-xs">
    <div class="col-xs-3">TOTAL ROUNDS: {{ rounds }}</div>
    <div class="col-xs-3 end-xs">YOU</div>
    <div class="col-xs-3">{{yourScore}} : {{computerScore}}</div>
    <div class="col-xs-3 start-xs">SHELDON</div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const Header = defineComponent({
  props: {
    rounds: Number,
    yourScore: Number,
    computerScore: Number,
  },
});

export default Header;
</script>
