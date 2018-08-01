<template>
    <li class="comment" transition="slide">
        <img class="comment__avatar" :src="avatar" alt="">
        <div class="comment__body">
            <p class="comment__name">
                {{ comment.name }}
                <span class="comment__date">
                  {{ comment.time }}
                </span>
            </p>
            <p class="comment__msg" v-html="comment.message"></p>
        </div>
    </li>
</template>

<script>
    export default {
    
        props: ['comment'],
    
        computed: {
            avatar: function() {
                return 'https://api.adorable.io/avatars/48/' + this.comment.name.toString().toLowerCase().trim().replace(/[\s\W-]+/g, '-') + '@adorable.io.png'
            }
        }
    }
</script>

<style lang='scss' scoped>
    @import "../scss/style.scss";
    .comment {
        padding: 30px 20px;
        border-bottom: 1px solid $gray-lightest;
        &:last-of-type {
            border-bottom: none;
        }
        &__avatar {
            float: left;
            height: 40px;
            margin-right: 11px;
            border-radius: 50%;
        }
        &__body {
            text-align: left;
            padding-left: 55px;
        }
        &__name {
            margin-bottom: 5px;
            font-size: $font-small;
            color: $primary;
            font-weight: 600;
        }
        &__msg {
            font-size: $font-small;
            padding-right: 25px;
        }
        &__date {
            float: right;
            font-size: $font-small;
            opacity: 0.5;
        }
    }
</style>