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
			tasks: [
				{
					name: 'Tarea 1',
					done: false
				},
				{
					name: 'Tarea 2',
					done: false
				},
				{
					name: 'Tarea 3',
					done: false
				}
			]
		}
	},
	methods: {
		toggleTasks (task) {
			task.done = !task.done
		},
		addTask () {
			if (!this.newTaskName) return
			this.tasks.push( {name:this.newTaskName, done:false} )
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