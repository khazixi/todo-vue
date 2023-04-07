<script setup lang="ts">
import { reactive, ref } from 'vue'
import type { Ref } from 'vue'

const ListItem: string[] = reactive([])
const placeholder: Ref<string> = ref('')
const editHolder: Ref<string> = ref('')
interface EditHold {
  msg: string
  idx: number
  active: boolean
}
const editPlaceholder: EditHold = reactive({
  msg: '',
  idx: 0,
  active: false
})

function addItem(item: string) {
  ListItem.push(item)
}

function removeItem(index: number) {
  ListItem.splice(index, 1)
}

function initializeEditItem(index: number, item: string) {
  editPlaceholder.idx = index
  editPlaceholder.msg = item
  editPlaceholder.active = true
}

function editItem() {
  // ListItem[editPlaceholder.idx] = editPlaceholder.msg
  ListItem[editPlaceholder.idx] = editPlaceholder.msg
  editPlaceholder.active = false
}
</script>

<template>
  <div>
    <h1>This is a list</h1>

    <ul>
      <li v-for="(item, index) in ListItem" :key="item">
        {{ item }}
        <button @click="removeItem(index)">Delete</button>
        <button @click="initializeEditItem(index, item)">Edit</button>
      </li>
    </ul>

    <p></p>

    <form @submit.prevent action="submit" id="TodoForm">
      <h2>Placehold Selector</h2>
      <input type="text" name="Sample" v-model="placeholder" />
      <input @click="addItem(placeholder)" type="submit" />
    </form>

    <form @submit.prevent v-if="editPlaceholder.active">
      <h2>Edit Selector</h2>
      <input type="text" name="Sample" v-model="editPlaceholder.msg" />
      <input @click="editItem()" type="submit" />
    </form>
  </div>
</template>
