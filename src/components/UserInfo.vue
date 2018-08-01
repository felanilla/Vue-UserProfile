<template>
    <div class="user">
        <img v-bind:src="shareImageSrc" @click="onShow(item)" class="user__share icon" alt="Share">
        <vodal :show="show" :animation="slideUp" @hide="show = false">
            <div class="vodal-header">{{userProfileSrc}}</div>
            <button class="button button--small vodal-confirm-btn" @click="show = false">ok</button>
        </vodal>
        <div>
            <img class="user__avatar" src="https://api.adorable.io/avatars/70/harvey@adorable.png" alt="User">
            <p class="user__name">
                {{firstName}} {{lastName}}
                <img v-bind:src="likeImageSrc" v-on:click="addLike" :class="{liked: isLiked}" class="user__heart icon" alt="Like">
            </p>
            <p class="user__location">
                {{location}}
            </p>
        </div>
        <div class="user__wrapper">
            <div class="user__socials">
                <div class="user__social">
                    <p id="likes" class="user__count">
                        {{likes}}
                    </p>
                    <span class="user__copy">
                            Likes
                        </span>
                </div>
                <span class="user__line"></span>
                <div class="user__social">
                    <p id="following" class="user__count">
                        {{following}}
                    </p>
                    <span class="user__copy">
                            Following
                        </span>
                </div>
                <span class="user__line"></span>
                <div class="user__social">
                    <p id="followers" class="user__count">
                        {{followers}}
                    </p>
                    <span class="user__copy">
                            Followers
                        </span>
                </div>
            </div>
            <a v-on:click="addFollower" :class="{followed: isFollowed}" class="user__button button button--big">
                    {{state}}
                </a>
        </div>
    </div>
</template>

<script>
    import Vue from 'vue';
    import Vodal from 'vodal';
    
    Vue.component(Vodal.name, Vodal);
    
    export default {
        name: 'UserInfo',
        data() {
            return {
                firstName: 'Harvey',
                lastName: 'Specter',
                location: 'New York, USA',
                likes: 121,
                following: 723,
                followers: 4433,
                state: '',
                isLiked: false,
                isFollowed: false,
                show: false,
                likeImageSrc: './src/assets/heart.svg',
                shareImageSrc: './src/assets/share.svg',
                userProfileSrc: 'https://felanilla.github.io/Vue-UserProfile',
            }
        },
        methods: {
            addLike: function() {
                this.isLiked = !this.isLiked
                if (this.isLiked == true) {
                    this.likes += 1
                    this.likeImageSrc = './src/assets/heart-active.svg'
                } else {
                    this.likes -= 1
                    this.likeImageSrc = './src/assets/heart.svg'
                }
            },
            addFollower: function() {
                this.isFollowed = !this.isFollowed
                if (this.isFollowed == true) {
                    this.followers += 1
                    this.state = "Unfollow"
                } else {
                    this.followers -= 1
                    this.state = "Follow"
                }
            },
            onShow(animation) {
                this.show = true;
            }
        },
        created: function() {
            this.isFollowed = !this.default
            this.addFollower()
        }
    }
</script>

<style lang='scss'>
    @import "../scss/style.scss";
    .user {
        position: relative;
        height: 235px;
        margin: 0 auto;
        background-color: $default;
        border-radius: 5px;
        box-shadow: $box-shadow;
        &__share {
            position: absolute;
            top: 15px;
            right: 15px;
            height: 15px;
        }
        &__avatar {
            position: absolute;
            width: 70px;
            height: 70px;
            top: -55px;
            left: 0;
            right: 0;
            margin-left: auto;
            margin-right: auto;
            border-radius: 50%;
            @include breakpoint(md) {
                position: relative;
                float: left;
                margin: 0 20px 0 0;
                top: 0;
            }
        }
        &__name {
            padding-top: 38px;
            font-size: $font-big;
            font-weight: 600;
            text-align: center;
            color: $primary;
            @include flexbox;
            @include justify-content(center);
            @include align-items(center);
            @include breakpoint(md) {
                padding-top: 15px;
                text-align: left;
                @include justify-content(flex-start);
            }
        }
        &__heart {
            height: 15px;
            margin-left: 10px;
        }
        &__location {
            color: $light;
            font-size: $font-xsmall;
            @include breakpoint(md) {
                text-align: left;
            }
        }
        &__socials {
            width: 90%;
            max-width: 280px;
            height: 42px;
            margin: 20px auto 0;
            @include flexbox;
            @include justify-content(space-between);
            @include align-items(center);
            @include breakpoint(sm) {
                width: 60%;
            }
        }
        &__count {
            color: $secondary;
            font-size: 24px;
            font-weight: 500;
        }
        &__copy {
            font-size: 10px;
            text-align: left;
            color: $light;
        }
        &__line {
            width: 1px;
            height: 20px;
            background-color: $gray-lighter;
            opacity: 0.1;
        }
        &__button {
            @include breakpoint(md) {
                width: 200px;
                margin-left: 30px;
            }
        }
        &__wrapper {
            @include breakpoint(md) {
                width: 100%;
                @include flexbox;
                @include align-items(center);
            }
        }
        @include breakpoint(md) {
            padding: 20px;
            height: 183px;
        }
    }
</style>
