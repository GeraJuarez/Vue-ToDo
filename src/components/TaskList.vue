<template>
    <div class="collection with-header">
		<ul>
            <li class="collection-header">
                <h3>{{ title }}</h3>
            </li>
			<li class="collection-item" v-for="(task, index) in taskList"
				:key="index">
				{{ task.name }} - {{ task.done ? 'Complete' : 'Pendiente' }}
				<button class="btn-small secondary-content" v-if="!task.done" type="button" @click="toggleTasks(task)">Completar</button>
			</li>
		</ul>
    </div>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            required: true
        },
        taskList: {
            type: Array,
            required: true
        }
    },
    methods: {
        toggleTasks (task) {
            this.$emit("completar", task)
        }
    }
}
</script>

