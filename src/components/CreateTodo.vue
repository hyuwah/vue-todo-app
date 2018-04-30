/* eslint-disable */
<template>
  <div class="ui basic content center aligned segment">
      <button class="ui basic button icon fab" v-on:click="openForm" v-show="!isCreating">
          <i class="plus icon"></i>
      </button>

      <div class="ui centered card" v-show="isCreating">
          <div class="content">
              <div class="ui form">
                  <div class="field">
                      <label>Title</label>
                      <input v-model="titleText" type="text" ref='title' directValue="">
                  </div>
                  <div class="field">
                      <label>Project</label>
                      <input v-model="projectText" type="text" ref='project' defaultValue="">
                  </div>
                  <div class="ui two buttons">
                      <button class="ui blue basic button" v-on:click="sendForm()">Create</button>
                      <button class="ui red basic button" v-on:click="closeForm">Cancel</button>
                  </div>
              </div>
          </div>
          <div class="extra content">
              <p style="text-align:right">All fields are required</p>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  
    data() {
        return {
          titleText: '',
          projectText: '',
          isCreating: false,
        };
    },

    methods: {
        openForm() {
          this.isCreating = true;
        },
        closeForm() {
          this.isCreating = false;
        },
        sendForm() {
            if (this.titleText.length > 0 && this.projectText.length > 0) {
                const title = this.titleText;
                const project = this.projectText;

                this.$emit('create-todo', {
                    title,
                    project,
                    done: false,
                });
                this.titleText='';
                this.projectText='';
                this.isCreating = false;
            }
        },
    },
};
</script>

<style scoped>
.fab {
}
</style>
