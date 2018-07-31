<template>
  <div id="app">
    <div class="user-profile">
        <user-info></user-info>
        <div class="comments">
          <span v-show="loading" class="spinner"></span>
          <ul class="comments__list">
              <comment v-for="comment in comments" :comment="comment"></comment>
          </ul>
           <comment-form v-on:commented="updateComment"></comment-form>
        </div>
    </div>
  </div>
</template>

<script>
import UserInfo from './UserInfo.vue'
import Comment from './Comment.vue'
import CommentForm from './CommentForm.vue'

export default {

    data () {
      return {
        comments: [],
        loading: false
      }
    },

    components: {
      Comment,
      CommentForm,
      UserInfo
    },

    created () {
        this.loading = true;

        // Fetch the comments 
        this.$http.get('http://localhost:3434').then((response) => {
            // success callback
            this.comments = response.data;
            this.loading = false;
        }, (response) => {
            // error callback
            console.error(response);
            this.loading = false;
        });
    },

    methods: {
      updateComment (comment) {
        this.comments.push(comment);
      } 
    }

}
</script>

<style lang='scss'>
  @import "../scss/style.scss";

  .user-profile {
    position: relative;
    max-width: 500px;
    height: 812px;
    margin: 25px auto;
    padding: 40px 18px;
    background-color: $default;
    border-radius: 5px 5px 0 0;
    box-shadow: 0 0 4px 0 rgba(172,172,172,0.50);

    &:before {
      display: block;
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 95px;
      background-color: $primary;
      border-radius: 5px 5px 0 0;
      box-shadow: 0 0 4px 0 rgba(172,172,172,0.50);
    }

    @include breakpoint(md) {
      height: 760px;
      margin: 60px auto;
    }
  }

  .comments {
    margin-top: 15px;
    padding-bottom: 30px;
    background-color: $default;
    box-shadow: $box-shadow;
    border-radius: 5px;

    &__list {
      max-height: 523px;
      overflow-x: scroll;
      border-bottom: 1px solid $gray-lightest;
      @include flexbox;
      @include flex-direction(column);
    }
  }
</style>