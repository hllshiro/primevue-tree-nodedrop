<template>
  <div class="card flex flex-col gap-4">
    <div class="p-4 bg-blue-50 border-l-4 border-blue-500 rounded text-sm">
      <strong>Goal:</strong> Prevent dropping nodes <u>INSIDE</u> a file (icon:
      pi-file), but allow dropping <u>ABOVE</u> or <u>BELOW</u> it as a sibling.
      <br />
      <strong>Current Issue:</strong> The <code>onNodeDrop</code> event doesn't
      tell us the drop position, making it impossible to tell the difference.
    </div>

    <Tree
      v-model:value="nodes"
      class="flex-1 border border-surface rounded-lg"
      draggableNodes
      droppableNodes
      valitdate-drop
      @node-drop="onNodeDrop"
    >
      <template #default="slotProps">
        <span>{{ slotProps.node.label }}</span>
      </template>
    </Tree>

    <div
      v-if="lastAction"
      class="p-2 border rounded bg-surface-100 text-xs font-mono"
    >
      Last Action Log: {{ lastAction }}
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const lastAction = ref("");
const nodes = ref([
  {
    key: "0-0",
    label: "src (Folder)",
    icon: "pi pi-fw pi-folder",
    children: [
      { key: "0-0-0", label: "App.vue (File)", icon: "pi pi-fw pi-file" },
      { key: "0-0-1", label: "main.js (File)", icon: "pi pi-fw pi-file" },
    ],
  },
  {
    key: "0-1",
    label: "package.json (File)",
    icon: "pi pi-fw pi-file",
  },
]);

const onNodeDrop = (event) => {
  const { dragNode, dropNode, index } = event;

  // PROBLEM: We want to intercept here.
  // If user tries to drop "src" INTO "package.json", it should be blocked.
  // If user tries to drop "src" ABOVE "package.json", it should be allowed.

  // CURRENT LIMITATION:
  // We only know 'dropNode' is 'package.json'.
  // We DON'T know if the drop indicator was a line (sibling) or a box (into).

  const isFile = dropNode.icon === "pi pi-fw pi-file";

  if (isFile) {
    // If we block here, we also accidentally block moving nodes to be
    // siblings of this file, which is bad UX.
    lastAction.value = `Dropped ${dragNode.label} on ${dropNode.label}. But is it INTO or BESIDE? We don't know.`;

    // How to implement: if (dropPosition === 0) { event.reject(); } ?
  }

  // PrimeVue default logic
  if (event.accept) event.accept();
};
</script>
