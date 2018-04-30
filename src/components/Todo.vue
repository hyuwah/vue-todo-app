<template>
   <div class='ui centered card'>

    <div class="content" v-show="!isEditing">
      <div class='header'>
          {{ todo.title }}
      </div>
      <div class='meta'>
          {{ todo.project }}
      </div>
      <div class='extra content'>
        <span class='right floated edit icon' v-on:click="showForm">
          <i class='edit icon'></i>
        </span>
        <span class="right floated trash icon" v-on:click="deleteTodo(todo)">
            <i class="trash icon"></i>
        </span>
      </div>
    </div>

    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Title</label>
          <input type='text' v-model="todo.title" >
        </div>
        <div class='field'>
          <label>Project</label>
          <input type='text' v-model="todo.project" >
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Close X
          </button>
        </div>
      </div>
    </div>
    <div class='ui bottom attached green basic button' v-show="!isEditing && todo.done" v-on:click="toggleComplete(todo)">
        Completed
    </div>
    <div class='ui bottom attached red basic button' v-show="!isEditing && !todo.done" v-on:click="toggleComplete(todo)">
        Pending
    </div>
  </div>
</template>

<script type="text/javascript">
export default {
  props: ['todo'],
  data() {
    return {
      isEditing: false,
    };
  },
  methods: {
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
    deleteTodo(todo) {
        swal({
            title: "Are you sure?",
            text: "This todo will be deleted forever!",
            icon: "warning",
            buttons: true,
            dangerMode: true,
        })
        .then((willDelete)=> {
            if(willDelete){
                swal('Successfully deleted', `${todo.title} deleted..`, 'success');
                this.$emit('delete-todo', todo);
            }
        });
    },
    toggleComplete(todo) {
        this.$emit('toggle-complete', todo)
    },
  },
};
</script>

<style>

</style>
