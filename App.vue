<template>
  <div class="container column">
    <resume-form @block-added="addBloks"></resume-form>
    <resume-view :blocks="blocks"></resume-view>

  </div>
  <div class="container">
    <app-loader v-if="loading"></app-loader>
    <resume-comments
    v-else
    :comments="comments"
    @load-comments="loadComments"
    ></resume-comments>
  </div>
</template>

<script>
import ResumeForm from './Components/ResumeForm.vue'
import ResumeView from './Components/ResumeView.vue'
import ResumeComments from './Components/ResumeComments.vue'
import AppLoader from './Components/AppLoader.vue'


export default {
  data() {
    return {
      blocks: [],
      comments: [],
      loading: false
    }
  },
  methods: {
    async loadComments(){
      this.loading = true
      const res = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42')
      this.comments = await res.json()
      this.loading = false
    },
    addBloks(block) {
      this.blocks.push(block)
    }
  },
  components: {ResumeForm, ResumeView, ResumeComments, AppLoader}
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
