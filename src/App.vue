<template>
  <div class="container">
    <!-- <Header @toggle-add-task="toggleAddTask" title="Task Tracker" /> -->
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask" />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" :showAddTask="showAddTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<script>
import Header from './components/Header';
import Tasks from './components/Tasks';
import AddTask from './components/AddTask'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map(task => (task.id === id ? { ...task, reminder: !task.reminder } : task));
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Camping Trip',
        day: 'October 1st at 2:00pm',
        reminder: true
      },
      {
        id: 2,
        text: 'Food Shopping',
        day: 'September 28th at 6:00pm',
        reminder: false
      },
      {
        id: 3,
        text: 'Car Inspection',
        day: 'September 29th at 8:00am',
        reminder: true
      }
    ];
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
  color: #333;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}

.fas {
  color: red;
  cursor: pointer;
}

.task {
  background: #f4f4f4;
  margin: 10px;
  padding: 0.75em;
  border: 1px solid #888;
}

.task.reminder {
  border-left: 5px solid green;
}

.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

/* .task .fas {
  display: inline-block;
  text-align: right;
} */
.task p {
  width: 80%;
}
</style>
