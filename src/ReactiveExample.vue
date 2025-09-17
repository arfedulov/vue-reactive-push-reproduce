<template>
  <div>
    <h2>example with reactive()</h2>
    <h3>items</h3>

    <button @click="addItem">1) add item</button>
    <button @click="addItemFromOutsideByPush">2) add item from outside by push</button>
    <button @click="addItemFromOutsideByReassign">3) add item from outside by reassign</button>

    <ul>
      <li v-for="item of myObject.items" :key="item">{{ item }}</li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { readonly, reactive} from "vue";

const useMyObject = () => {
  const myObject = reactive({
    items: ['one', 'two', 'three']
  })

  const addItem = () => {
    myObject.items.push(`item_${Date.now()}`)
  }

  return {
    myObject: readonly(myObject),
    addItem,
  }
}

const { myObject, addItem } = useMyObject()

const addItemFromOutsideByPush = () => {
  myObject.items.push(`item_${Date.now()}`)
}

const addItemFromOutsideByReassign = () => {
  myObject.items = [...myObject.items, `item_${Date.now()}`]
}
</script>