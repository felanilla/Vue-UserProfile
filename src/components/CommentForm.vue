<template>
  <div id="comment">
        <div class="loader" v-show="loading" >
          <span class="spinner"></span>  
        </div>
        <form action="" method="post" @submit.prevent="submit">
          <textarea v-model="data.message" class="input input--bottom" name="message" id="message" rows="1" placeholder="Add a comment" required></textarea>
          <span class="input-line"></span>
          <input v-model="data.name" class="input input--bottom" type="text" name="name" placeholder="Your Name" required>
          <span class="input-line"></span>
          <input class="button button--big" :disabled="loading" type="submit" value="Comment">
        </form>
    </div>
</template>

<script>
export default {

    data() {
      return {
        loading: false,
        data: {}
      }
    },

    methods: {
      submit() {
        this.loading = true;

        this.$http.post('http://localhost:3434', this.data).then((response) => {
          this.$emit('commented', response.data);  
          this.data.message = "";
          this.loading = false;
        }, (response) => {
          this.loading = false;
        });
      }
    }

}
</script>

<style lang='scss' scoped>
@import "../scss/style.scss";

  .button {
    margin-top: 40px;
  }

  #comment {
    position: relative;
  }

  #comment .spinner {
    margin-top: 5em;
    z-index: 999;
  }

  #comment .loader {
    content: '';
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    background-color: rgba(255, 255, 255, 0.8);
    z-index: 2;
  }
</style>