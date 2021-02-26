<template>
    <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
      <div class='text-icons'>
          <div v-if="editing === task.id">
            <input type="text" v-model="task.text" />
          </div>
          <h3 v-else>{{ task.text }}</h3>

          <div v-if="editing === task.id" class="icons">
              <i @click="editTask(task)" class="fa fa-check" aria-hidden="true"></i>
              <i @click="editing = null" class="fas fa-times"></i>
          </div>

          <div v-else class="icons">
              <i @click="editMode(task.id)" class="fa fa-edit"></i>
              <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
            </div>        
      </div>

        <div v-if="editing === task.id">
          <input type="text" v-model="task.day" />
        </div>
        <p v-else>{{ task.day }}</p>
    </div>

</template>

<script>
    export default {
        name: 'Task',
        props: {
            task: Object
        },
        data() {
          return {
            editing: null
          }
        },
        methods: {
            editMode(id) {
              this.editing = id
            },
          editTask(task) {
            if (task.text === '' || task.day === '') return
            this.$emit('edit-clicked')
            this.editing = null
          }
        }
    }
</script>

<style scoped>
.fas {
  color: red;
  margin-left: 5px;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}

.text-icons {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.icons {
  font-size: 25px;
}

</style>