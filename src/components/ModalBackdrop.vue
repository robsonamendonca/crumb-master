<template>
  <div
    v-if="showModal"
    class="modal-backdrop"
    @click="closeModal"
  />
</template>

<script>
import { EventBus } from '../util/EventBus.js';

export default {
  name: 'ModalBackdrop',
  data() {
    return {
      showModal: false,
    };
  },
  mounted() {
    EventBus.$on('showModal', () => {
      this.showModal = true;
    });

    EventBus.$on('closeModal', () => {
      this.showModal = false;
    });
  },
  methods: {
    closeModal() {
      EventBus.$emit('closeModal');
    },
  },
};
</script>

<style lang="scss">
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    opacity: 0.5;
  }

  .light .modal-backdrop {
    background-color: $black;
  }

  .dark .modal-backdrop {
    background-color: $white;
  }
</style>
