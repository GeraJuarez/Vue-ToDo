<template>
	<div class="container">
		<div class="row">
			<div class="col s6 offset-s3">
				<h1 class="center-align">My TO DO app</h1>
				<form class="center-align" @submit.prevent="addTask">
					<input placeholder="Nueva tarea" id="task" v-model="newTaskName" type="text">
					<input class="btn" type="submit" value="Agrega tarea">
				</form>
			</div>
		</div>	

		<div class="row">
			<div class="col s6">
				<task-list 
				:title="'Pendientes Prueba'"
				:task-list="tasksPending"
				@completar="toggleTasks"/>
			</div>
			<div class="col s6">
				<task-list 
				:title="'Completados Prueba'"
				:task-list="tasksComplete"
				@completar="toggleTasks"/>	
			</div>
		</div>
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
