<template>
	<div class="home">
		<button class="btn-rounded" @click="handleCreateTask">Create New Task Item</button>
		<ul class="margin-top wrapper" v-if="tasks.length">
			<li v-for="(task, id) in tasks" :key="id" :class="{'checked' : task.checked}">
				<strong style="width: 30%; text-align: left">{{task.title}} </strong>
				<span style="width: 40%; text-align: left">{{task.task}}</span>
				<div class="" style="width: 30%;">
					<input type="checkbox" id="i" v-model="task.checked">
					<span class="margin-left cursor error" @click="handlerDeleteTask(task.id)">Delete</span>
					<span class="margin-left cursor success" @click="handleEditTask(task)">Edit</span>
				</div>
			</li>
		</ul>
		<dialog-menu v-if="dialog" @confirm="confirmAction"/>
		<edit-item :item="task" @action="handleEditItem"/>

	</div>
</template>

<script>


  import DialogMenu from "../components/dialogMenu";
  import EditItem from "../components/editItem";

  export default {
    name: 'Home',
    components: {EditItem, DialogMenu},
    data() {
      return {
        tasks: [],
        dialog: false,
        confirm: false,
        item: '',
        task: null,
      }
    },
    mounted() {
      if (JSON.parse(localStorage.getItem('tasks'))) {
        this.tasks = JSON.parse(localStorage.getItem('tasks'))
      }
    },
    methods: {
      saveToLocalStorage(key, item) {
        localStorage.setItem(key, JSON.stringify(item))
      },
      handleCreateTask() {
        this.$router.push('/create-new')
      },
      confirmAction(e) {
        if (e && this.confirm === 'delete') {
          this.deleteAction()
        }
        this.dialog = false
        this.id = null
        console.log(e)
      },
      handlerDeleteTask(id) {
        this.dialog = true
        this.confirm = 'delete'
        this.id = id
        console.log(this.dialog)
      },
      handleEditTask(task) {
        this.task = task
      },
      handleEditItem(e) {
        console.log(e, 'handleEditItem')
        if (e) {
          this.saveToLocalStorage('tasks', this.tasks)
        } else {
          this.tasks = JSON.parse(localStorage.getItem('tasks'))
        }
        this.task = null
      },
      deleteAction() {
        let arr = this.tasks.filter(el => el.id !== this.id)
        this.saveToLocalStorage('tasks', arr)
        this.tasks = JSON.parse(localStorage.getItem('tasks'))
      }
    }

  }

</script>
<style lang="scss" scoped>
	.checked {
		text-decoration: line-through;
	}

	.margin--left {
		margin-left: 10px;
	}
</style>