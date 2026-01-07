<template>
    <ThemeSwitcher />
    <div class="card flex flex-col md:flex-row gap-4">
        <Tree v-model:value="value1" class="flex-1 border border-surface rounded-lg" draggableNodes droppableNodes draggableScope="first" droppableScope="none" validate-drop>
            <template #empty> No Items Left </template>
        </Tree>
        <Tree v-model:value="value2" class="flex-1 border border-surface rounded-lg" draggableNodes droppableNodes draggableScope="second" droppableScope="first" validate-drop>
            <template #empty> Drag Nodes Here </template>
        </Tree>
        <Tree v-model:value="value3" class="flex-1 border border-surface rounded-lg" draggableNodes droppableNodes :droppableScope="['first', 'second']" validate-drop>
            <template #empty> Drag Nodes Here </template>
        </Tree>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const value1 = ref([
    {
        key: '0-0',
        label: '.github',
        data: '.github folder',
        icon: 'pi pi-fw pi-folder',
        children: [
            {
                key: '0-0-0',
                label: 'workflows',
                data: 'workflows folder',
                icon: 'pi pi-fw pi-folder',
                children: [
                    {
                        key: '0-0-0-0',
                        label: 'node.js.yml',
                        data: 'node.js.yml file',
                        icon: 'pi pi-fw pi-file'
                    }
                ]
            }
        ]
    },
    {
        key: '0-1',
        label: '.vscode',
        data: '.vscode folder',
        icon: 'pi pi-fw pi-folder',
        children: [
            {
                key: '0-1-0',
                label: 'extensions.json',
                data: 'extensions.json file',
                icon: 'pi pi-fw pi-file'
            }
        ]
    },
    {
        key: '0-2',
        label: 'public',
        data: 'public folder',
        icon: 'pi pi-fw pi-folder',
        children: [
            {
                key: '0-2-0',
                label: 'vite.svg',
                data: 'vite.svg file',
                icon: 'pi pi-fw pi-file'
            }
        ]
    },
    {
        key: '0-3',
        label: 'src',
        data: 'src folder',
        icon: 'pi pi-fw pi-folder',
        children: [
            {
                key: '0-3-0',
                label: 'assets',
                data: 'assets folder',
                icon: 'pi pi-fw pi-folder',
                children: [
                    {
                        key: '0-3-0-0',
                        label: 'vue.svg',
                        data: 'vue.svg file',
                        icon: 'pi pi-fw pi-file'
                    }
                ]
            },
            {
                key: '0-3-1',
                label: 'components',
                data: 'components folder',
                icon: 'pi pi-fw pi-folder',
                children: [
                    {
                        key: '0-3-1-0',
                        label: 'HelloWorld.vue',
                        data: 'HelloWorld.vue file',
                        icon: 'pi pi-fw pi-file'
                    }
                ]
            },
            {
                key: '0-3-2',
                label: 'App.vue',
                data: 'App.vue file',
                icon: 'pi pi-fw pi-file'
            },
            {
                key: '0-3-3',
                label: 'main.js',
                data: 'main.js file',
                icon: 'pi pi-fw pi-file'
            },
            {
                key: '0-3-4',
                label: 'style.css',
                data: 'style.css file',
                icon: 'pi pi-fw pi-file'
            }
        ]
    },
    {
        key: '0-4',
        label: 'index.html',
        data: 'index.html file',
        icon: 'pi pi-fw pi-file'
    },
    {
        key: '0-5',
        label: 'package.json',
        data: 'package.json file',
        icon: 'pi pi-fw pi-file'
    },
    {
        key: '0-6',
        label: 'vite.config.js',
        data: 'vite.config.js file',
        icon: 'pi pi-fw pi-file'
    }
]);

const value2 = ref([
    {
        key: '1-0',
        label: '/etc',
        icon: 'pi pi-fw pi-folder'
    }
]);

const value3 = ref([]);

</script>
