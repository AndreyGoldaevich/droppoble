
<template>
  <div class="container">
    <div v-for="category in categories"
      :key="category.id"
      @drop="onDrop($event, category.id)"
      class="droppable"
      @dragover.prevent
      @dragenter.prevent>
      <h4>{{ category.title }}</h4>
      <div v-for="item in items.filter(x => x.categoryId === category.id)"
        @dragstart="onDragStart($event, item)"
        class="draggable"
        draggable="true">
        <h5>{{ item.title }}</h5>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  name: 'App',
  setup() {
    const items = ref([
      {
        id: 0,
        title: 'Lond',
        categoryId: 0
      },
      {
        id: 1,
        title: 'longBow',
        categoryId: 0
      },
      {
        id: 2,
        title: 'fast machine',
        categoryId: 1
      },
      {
        id: 3,
        title: 'Google',
        categoryId: 2
      },
      {
        id: 4,
        title: 'Yandex',
        categoryId: 2
      },
    ])
    const categories = ref([
      {
        id: 0,
        title: 'Arow'
      },
      {
        id: 1,
        title: 'Hobbi'
      },
      {
        id: 2,
        title: 'Job'
      },
    ])
    function onDragStart(e, item) {
      e.dataTransfer.dropEffect = 'move'
      e.dataTransfer.effectAllowed = 'move'
      e.dataTransfer.setData('itemId', item.id.toString())
    }
    function onDrop(e, categoryId) {
      const itemId = parseInt(e.dataTransfer.getData('itemId'))
      items.value = items.value.map(x => {
        if (x.id == itemId)
          x.categoryId = categoryId
        return x
      })
    }
    return {
      items,
      categories,
      onDragStart,
      onDrop
    }
  }
}
</script>

<style scoped>
.container {
  width: 500px;
  margin: 0 auto;
  padding: 15px;
}
.droppable {
  padding: 15px;
  border-radius: 5px;
  background: #17a4ab;
  margin-bottom: 10px;
}
.droppable h4 {
  font-size: 30px;
  color: white;
}
.draggable {
  background: white;
  padding: 5px;
  border-radius: 5px;
  margin-bottom: 5px;
}
.draggable h5 {
  margin: 0;
  font-size: 18px;
}
</style>