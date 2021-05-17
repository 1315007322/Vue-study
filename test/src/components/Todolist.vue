<template>
  <div class="header">
    <input
      type="text"
      id="text"
      v-on:keyup.enter="handAdd"
      :value="currentValue"
    />
    <h2>todoList</h2>
    <ul v-for="(item, index) in todolist" :key="item.id">
      <li>
        <input type="checkbox" @click="handChoose(index)" />
        <span>
          {{ item.value }}
        </span>
        ----------
        <button @click="removeItem(index, todolist)"> - </button>
      </li>
    </ul>
    <h2>doneList</h2>
    <ul v-for="(item, index) in donelist" :key="item.id">
      <li>
        <input type="checkbox" checked @click="handcancel(index)" />
        <span>
          {{ item.value }}
        </span>
        ----------
        <button @click="removeItem(index, donelist)"> - </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'todolist',
  data () {
    return {
      count: 1,
      currentValue: '',
      todolist: [{id: 1, value: '吃早饭'}],
      donelist: []
    }
  },
  methods: {
    handAdd (e) {
      const value = e.target.value
      this.currentValue = ''
      this.todolist.push({id: ++this.count, value})
    },
    handChoose (index) {
      const value = this.todolist[index]
      this.todolist.splice(index, 1)
      this.donelist.push(value)
    },
    handcancel (index) {
      const value = this.donelist[index]
      this.todolist.splice(value.id - 1, 0, value)
      this.donelist.splice(index, 1)
    },
    removeItem (index, arr) {
      arr.splice(index, 1)
    }
  }
}
</script>

<style scoped>
li {
  list-style: none;
}
</style>
