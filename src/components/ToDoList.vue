<template>
  <div class="container">
    <h3 class="title">{{title}} {{completedToDoCount}} of {{toDoCount}} items complete</h3>
    <ul class="todo-list">
      <slot></slot>
    </ul>
  </div>
</template>


<script>
export default {
  name: "ToDoList",
  props: ["title"],
  data: function () {
    return {
      toDoCount: 0,
      completedToDoCount: 0,
    };
  },
  mounted: function () {
    this.updateToDoCount();
  },
  updated: function () {
    this.updateToDoCount();
  },
  methods: {
    updateToDoCount: function () {
      this.toDoCount = this.$slots.default.filter((todo) => todo?.componentInstance).length || 0;

      let completedList = this.$slots.default.filter(
        (todo) => todo?.data?.model?.value && todo?.componentInstance
      );

      this.completedToDoCount = completedList.length || 0;
    },
  },
};
</script>

<style scoped>
.todo-list {
  list-style-type: none;
}
.container{
  margin:2rem
}
</style>


