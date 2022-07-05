<template>
  <button class='btn_common' @click="handleOpenModalDetail()"><i :class="icon"></i> {{ nameBtn }}</button>
</template>

<script>
import { EventBus } from '../../EventBus'

export default {
  name: 'ButtonDetail',
  props: {
    nameBtn: String,
    icon: String
  },
  methods: {
    handleOpenModalDetail() {
      EventBus.$emit('open-modal-in-detail', this.nameBtn);
    }
  }
}
</script>

<style scoped>
.btn_common {
  padding: 5px 35px;
  border: none;
  border-radius: 4px;
  margin: 5px 0;
  width: 200px;
}
</style>