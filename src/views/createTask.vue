<template>
	<div class="main-wrapper">
		<router-link to="/" class="navigate-back">Back</router-link>

		<form class="wrapper " @submit.prevent="handlerSaveTask">
			<p class="width-100 flex">
				<span :class="{'error' : titleError}">Title: </span>
				<input type="text"
							 id="title"
							 v-model="title"
							 class="border-bottom margin-left flex-grow"></p>
			<p class="width-100 flex margin-top">
				<span :class="{'error' : taskError}">	Task: </span>
				<input type="text"
							 id="task"
							 v-model="task"
							 class="border-bottom margin-left flex-grow">
			</p>

			<button type="submit" class="btn-rounded">Save</button>
		</form>
	</div>

</template>

<script>
  export default {
    name: "createTask",
    data() {
      return {
        title: '',
        titleError: false,
        task: '',
        taskError: false,

      }
    },
    methods: {
      validate() {
        if (this.title.length && this.task.length) {
          this.titleError = false
          this.taskError = false
          return true
        }
        this.titleError = !this.title.length;
        this.taskError = !this.task.length;

      },
      saveToLocalStorage(key, item) {
        localStorage.setItem(key, JSON.stringify(item))
      },
      localStorageGetItem(key) {
        return JSON.parse(localStorage.getItem(key))
      },
      handlerSaveTask() {
        let resp = this.validate()
        if (resp) {
          let obj = {
            title: this.title,
            task: this.task,
            checked: false,
          }
          let tasks = this.localStorageGetItem('tasks')
          if (tasks) {
            obj.id = tasks.length
            tasks.push(obj)
            this.saveToLocalStorage('tasks', tasks)
          } else {
            let arr = []
            obj.id = arr.length
            arr.push(obj)
            this.saveToLocalStorage('tasks', arr)
          }
        }
        this.$router.push('/')
      }
    }
  }
</script>
