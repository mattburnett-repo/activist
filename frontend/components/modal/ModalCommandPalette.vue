<template>
  <ModalBase
    @closeModal="handleCloseModal"
    :isOpen="modalShouldClose == false ? modalIsOpen : false"
  >
    <div>
      <button
        @click="_isOpen = true"
        class="rounded bg-blue-500 p-2 text-white"
      >
        Open Command Palette
      </button>

      <TransitionRoot :show="_isOpen" as="template">
        <Dialog
          @close="_isOpen = false"
          as="div"
          class="fixed inset-0 z-50 overflow-y-auto"
        >
          <div class="flex min-h-screen items-center justify-center px-4">
            <DialogOverlay class="fixed inset-0 bg-black opacity-50" />

            <span class="inline-block h-screen align-middle" aria-hidden="true"
              >&#8203;</span
            >

            <div
              class="my-8 inline-block w-full max-w-md transform overflow-hidden rounded-lg bg-white p-6 text-left align-middle shadow-xl transition-all"
            >
              <DialogTitle class="text-lg font-medium leading-6 text-gray-900"
                >Command Palette</DialogTitle
              >

              <Combobox v-model="selectedCommand" @change="handleCommand">
                <div class="relative mt-4">
                  <div
                    class="relative w-full cursor-default rounded-lg bg-white text-left shadow-md focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:ring-offset-gray-100 sm:text-sm"
                  >
                    <ComboboxInput
                      @keydown.enter="handleEnter"
                      class="w-full border-none py-2 pl-3 pr-10 text-sm leading-5 text-gray-900 placeholder-gray-400 focus:ring-0"
                      placeholder="Type a command..."
                    />
                  </div>

                  <Transition
                    as="div"
                    enter="transition ease-out duration-100"
                    enterFrom="opacity-0 scale-95"
                    enterTo="opacity-100 scale-100"
                    leave="transition ease-in duration-75"
                    leaveFrom="opacity-100 scale-100"
                    leaveTo="opacity-0 scale-95"
                  >
                    <ComboboxOptions
                      class="absolute z-50 mt-1 max-h-60 w-full overflow-auto rounded-md bg-white shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm"
                    >
                      <ComboboxOption
                        v-for="command in filteredCommands"
                        v-slot="{ active }"
                        :key="command.id"
                        :value="command"
                        as="li"
                      >
                        <li
                          :class="[
                            'relative cursor-pointer select-none py-2 pl-10 pr-4',
                            active
                              ? 'bg-indigo-600 text-white'
                              : 'text-gray-900',
                          ]"
                        >
                          {{ command.name }}
                        </li>
                      </ComboboxOption>
                    </ComboboxOptions>
                  </Transition>
                </div>
              </Combobox>
            </div>
          </div>
        </Dialog>
      </TransitionRoot>
    </div>
  </ModalBase>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";
import {
  Dialog,
  DialogOverlay,
  DialogTitle,
  TransitionRoot,
} from "@headlessui/vue";
import {
  Combobox,
  ComboboxInput,
  ComboboxOptions,
  ComboboxOption,
} from "@headlessui/vue";

interface Command {
  id: number;
  name: string;
  action: () => void;
}

const commands: Command[] = [
  { id: 1, name: "Open Settings", action: () => console.log("Open Settings") },
  { id: 2, name: "Open Profile", action: () => console.log("Open Profile") },
  { id: 3, name: "Logout", action: () => console.log("Logout") },
];

const props = defineProps<{
  isOpen: boolean;
}>();

const _isOpen = ref(true);
const searchTerm = ref("");
const selectedCommand = ref<Command | null>(null);

const modalIsOpen = computed(() => props.isOpen);
const modalShouldClose = ref(false);

const emit = defineEmits(["closeModal"]);
const handleCloseModal = () => {
  modalShouldClose.value = true;
  emit("closeModal");
  modalShouldClose.value = false;
};

const filteredCommands = computed(() => {
  return commands.filter((command) =>
    command.name.toLowerCase().includes(searchTerm.value.toLowerCase())
  );
});

const handleEnter = () => {
  if (selectedCommand.value) {
    selectedCommand.value.action();
    _isOpen.value = false;
  }
};

const handleCommand = (command: Command) => {
  command.action();
  _isOpen.value = false;
};
</script>

<style scoped>
/* Add any additional custom styles here if needed */
</style>
