<template>
  <div>
    <h1>TODOリスト</h1>
    <h2>{{ new Date() | moment }}</h2>
    <div class="notDone">
      <h2>未完</h2>
      <div v-for="nd in notDone" :key="nd.name">
        <div class="task">
          {{ nd.name }} {{ nd.dead | moment }}
          <button @click="finish(nd)">finish</button>
          <button @click="del(nd)">delete</button>
        </div>
      </div>
    </div>
    <div class="done">
      <h2>完了済み</h2>
      <div v-for="d in done" :key="d.name">
        <div class="task">{{ d.name }} {{ d.time | moment }}</div>
      </div>
    </div>
    <div>
      <h2>追加</h2>
      <label>タスク名</label><input type="text" v-model="newTaskName" />
      <label>期限</label><input type="date" v-model="newTaskDeadline" />
      <button @click="add">add</button>
    </div>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "Task",
  data() {
    return {
      notDone: [
        { name: "線形", dead: new Date("2019-6-12") },
        { name: "文系", dead: new Date("2019-6-3") }
      ],
      done: [
        { name: "位相", time: new Date("2019-6-5") },
        { name: "演習", time: new Date("2019-5-31") }
      ],
      newTaskName: "",
      newTaskDeadline: new Date()
    };
  },
  methods: {
    add() {
      if (this.newTaskName != "") {
        this.notDone.push({
          name: this.newTaskName,
          dead: this.newTaskDeadline
        });
        this.newTaskName = "";
        this.newTaskDeadline = new Date();
      }
    },
    finish(nd) {
      this.notDone.splice(this.notDone.indexOf(nd), 1);
      this.done.push({ name: nd.name, time: new Date() });
    },
    del(nd) {
      this.notDone.splice(this.notDone.indexOf(nd), 1);
    }
  },
  filters: {
    moment: function(date) {
      return moment(date).format("YYYY/MM/DD");
    }
  }
};
</script>

<style></style>
