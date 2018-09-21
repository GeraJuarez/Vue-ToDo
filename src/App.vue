<template>
	<div>		
		<h1>My TO DO app</h1>
		<form @submit.prevent="addTask">
			<input v-model="newTaskName" type="text">
			<input type="submit" value="Agrega tarea">
		</form>

		<task-list 
		:title="'Pendientes Prueba'"
		:task-list="tasksPending"
		@completar="toggleTasks"/>
		<hr>

		<task-list 
		:title="'Completados Prueba'"
		:task-list="tasksComplete"
		@completar="toggleTasks"/>
	</div>
</template>

<script>
import TaskList from './components/TaskList'

export default {
	components: {
		TaskList
	},
	data () {
		return {
			newTaskName:'',
			tasks: [],
		}
	},
	mounted: function() {
		if (localStorage.getItem('tasks')) {
			this.tasks = JSON.parse(localStorage.getItem('tasks'));
		}
	},
	watch: {
		tasks: {
			handler() {
				localStorage.setItem('tasks', JSON.stringify(this.tasks));
			},
			deep: true,
		}
  	},
	methods: {
		toggleTasks (task) {
			task.done = !task.done
		},
		addTask () {
			if (!this.newTaskName) return
			let taskObject = {name:this.newTaskName, done:false}
			this.tasks.push( taskObject )
			this.newTaskName = ''
		}
	},
	computed: {
		tasksPending () {
			return this.tasks.filter(task => !task.done)
		},
		tasksComplete () {
			return this.tasks.filter(task => task.done)
		}
	}
}
</script>
