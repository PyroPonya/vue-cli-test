<template>
  <div class="list">
    <div class="list__header">
      <div class="header__name border" @click="sortWithKey(userList, 'name')">
        Имя
      </div>
      <div class="header__phone border" @click="sortWithKey(userList, 'phone')">
        Телефон
      </div>
    </div>
    <div class="list__body">
      <div
        class="body__element"
        v-for="(item, i) in hierarchy(userList)"
        :key="i"
      >
        <div class="border">{{ item.name }}</div>
        <div class="border">{{ item.phone }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'List',
  props: ['userList'],
  data () {
    return {}
  },
  methods: {
    hierarchy: (
      data = [],
      { idKey = 'id', parentKey = 'parent', childrenKey = 'children' } = {}
    ) => {
      const tree = []
      const childrenOf = {}
      data.forEach(item => {
        const { [idKey]: id, [parentKey]: parentId = 0 } = item
        childrenOf[id] = childrenOf[id] || []
        item[childrenKey] = childrenOf[id]
        parentId
          ? (childrenOf[parentId] = childrenOf[parentId] || []).push(item)
          : tree.push(item)
      })
      return tree
    },
    sortWithKey (arr, key) {
      if (key === 'name') {
        arr.sort(function (a, b) {
          if (a.name > b.name) {
            return 1
          }
          if (a.name < b.name) {
            return -1
          }
          return 0
        })
      }
      if (key === 'phone') {
        arr.sort(function (a, b) {
          if (a.phone > b.phone) {
            return 1
          }
          if (a.phone < b.phone) {
            return -1
          }
          return 0
        })
      }
    }
  }
}
</script>

<style scoped>
.list {
  width: 300px;
}
.list__header {
  display: grid;
  grid-template-columns: 1fr 1fr;
  cursor: pointer;
  background-color: rgba(128, 128, 128, 0.37);
}
.list__element {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.list__body {
  display: flex;
  flex-direction: column;
}
.body__element {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.border {
  border: 1px solid black;
}
</style>
