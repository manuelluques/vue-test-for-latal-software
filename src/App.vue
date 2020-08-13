<template>
<todo-list title="MyTodoListName">
        <todo-list-item title="My item 1" v-model="itemOneIsChecked" subtitle="My item 1 description">    
        </todo-list-item>
 
        <todo-list-item title="My item 2" v-model="itemTwoIsChecked" subtitle="My item 2 description">
        </todo-list-item>
 
        <todo-list-item title="My item 3" v-model="itemThreeIsChecked" subtitle="My item 3 description">
        </todo-list-item>
 
        <todo-list-item v-if="threeSecondsHasPassed" title="My item 4" v-model="itemFourIsChecked" subtitle="My item 4 description">
        </todo-list-item>
 
    </todo-list>
</template>

<script>
import ToDoList from './components/ToDoList'; 
import ToDoListItem from './components/ToDoListItem'; 

export default {
  name: "App",
  components: {
    "todo-list": ToDoList,
    "todo-list-item": ToDoListItem
  },
  data: function () {
    return {
      itemOneIsChecked: false,
      itemTwoIsChecked: true,
      itemThreeIsChecked: false,
      itemFourIsChecked: false,
      threeSecondsHasPassed: false,
    };
  },
  mounted: function () {
    setTimeout(() => {
      this.threeSecondsHasPassed = true; // After 3 seconds the 4th item should appear
    }, 3000),
      setTimeout(() => {
        this.itemOneIsChecked = !this.itemOneIsChecked; // After 5 seconds the 1st items check value will invert
      }, 5000);
  },
};
</script>

<style></style>
