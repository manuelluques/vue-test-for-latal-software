<template>
  <div class="container">
    <h3 class="title">{{title}} {{completeToDoCount}} of {{toDoCount}} items complete</h3>
    <button class="btn" @click="markAllAsComplete()">Mark all as complete</button>
    <button class="btn" @click="markAllAsIncomplete()">Mark  all as incomplete</button>
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
      completeToDoCount: 0,
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
      this.toDoCount =
        this.$slots.default?.filter((toDo) => toDo?.componentInstance)?.length || 0;

      let completedList = this.$slots.default.filter(
        (toDo) => toDo?.data?.model?.value && toDo?.componentInstance
      );

      this.completeToDoCount = completedList?.length || 0;
    },
    markAllAsComplete: function () {
      this.$slots.default.forEach((toDo) => {
        if (toDo.componentInstance?.updateValue) toDo.componentInstance.updateValue(true);
      });
    },
    markAllAsIncomplete: function () {
      this.$slots.default.forEach((toDo) => {
        if (toDo.componentInstance) toDo.componentInstance.updateValue(false);
      });
    },
  },
};
</script>

<style scoped>
.todo-list {
  list-style-type: none;
}
.container {
  margin: 2rem;
}

.btn{
margin: 0.5rem
}
</style>


