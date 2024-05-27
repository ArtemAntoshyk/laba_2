<template>
  <div class="d-flex flex-column gap-2">
    <ul class="list-group rounded-0">
      <to-do-item
        v-for="(item, index) in items"
        :key="index"
        :item="item"
        :index="index"
        @checked="handleChecked"
      />                   
    </ul>
    <to-do-new v-if="isCreate" @cancel="cancel" @success="addItem"/>
    <to-do-create v-else @create="isCreate = true"/>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import ToDoItem from './ToDoItem.vue';
import ToDoCreate from './ToDoCreate.vue';
import ToDoNew from './ToDoNew.vue';

const items = ref([
  { label: 'Task list and assignments', checked: false },
  { label: 'Set due date and assignments', checked: false },
  { label: 'Remove duplicate tasks and stories', checked: false },
  { label: 'Update the userflow and stories', checked: false },
  { label: 'Adjust the components', checked: false }
])
const isCreate= ref(false)

const cancel = () => {
  isCreate.value = false
}

const addItem = (newItem) => {
  items.value.push(newItem)
  cancel()
}

const handleChecked = (value: boolean, index: number) => {
  const newItem = items.value[index]
  newItem.checked = value
  items.value[index] = newItem
}
</script>