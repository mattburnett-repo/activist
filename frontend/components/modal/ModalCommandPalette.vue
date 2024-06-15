<template>
  <ModalBase
    @closeModal="handleCloseModal"
    :isOpen="modalShouldClose == false ? modalIsOpen : false"
  >
    <!-- <div
      class="focus-inside elem-shadow-sm my-2.5 flex w-[90%] grow select-none items-center justify-between rounded-md bg-light-layer-2 px-2 py-1 text-left text-light-distinct-text transition duration-200 dark:bg-dark-layer-2 dark:text-dark-distinct-text"
    > -->
    <Command theme="algolia">
      <Command.Input placeholder="Type a command or search..." />
      <Command.List>
        <Command.Empty>No results found.</Command.Empty>

        <Command.Group heading="Letters">
          <Command.Item>a</Command.Item>
          <Command.Item>b</Command.Item>
          <Command.Separator />
          <Command.Item>c</Command.Item>
        </Command.Group>

        <Command.Item>Apple</Command.Item>
      </Command.List>
    </Command>
    <!-- </div> -->
  </ModalBase>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { Command } from "vue-command-palette";

// TODO: maybe get rid of isOpen, modalIsOpen and modalShouldClose, since all we really
//  need is the 'closeModal' emit in 'handleCloseModal'
const props = defineProps<{
  isOpen: boolean;
}>();
const modalIsOpen = computed(() => props.isOpen);
const modalShouldClose = ref(false);

const emit = defineEmits(["closeModal"]);
const handleCloseModal = () => {
  emit("closeModal");
};
</script>

<style>
@import "components/commandPalette/algolia.css";
</style>
