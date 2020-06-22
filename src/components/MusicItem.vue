<template>
    <div v-bind:class="{music_itemon: index % 2 == 0}" class="music_item">
        <div class="item-title">
            <img v-on:click="play_pause" v-bind:src=icon_src alt="Start">
            <div>
                <div class="title-author">{{music.author}}</div>
                <div>{{music.title}}</div>
            </div>
        </div>
        <div class="music-time">{{music.audio.duration | minutes}}</div>
    </div>
</template>

<script>
    export default {

        name: "MusicItem",

        props: {
            music: {
                type: Object
            },
            index: Number,
            isplay_w: Boolean,
            pre_id: Number,

            id: Number,


        },
        data() {
            return {
                icon_src: require('@/assets/play.png'),
                current: {},
                previndex: 0,
                isplay: false

            }
        },

        watch: {
            id() {
                if (this.isplay == true) {
                    if (this.pre_id == this.index) {
                        if (this.isplay == false) {
                            this.icon_src = require('@/assets/pause.png');
                            this.isplay = true;


                        } else {
                            this.icon_src = require('@/assets/play.png')
                            this.isplay = false;
                        }
                    }
                } else {
                    if (this.id == this.index) {
                        this.icon_src = require('@/assets/pause.png');
                        this.isplay = true;
                    }
                }
            },

            isplay_w() {
                if (this.id == this.index) {
                    if (this.isplay_w == false) {
                        this.icon_src = require('@/assets/play.png');


                    } else {
                        if (this.isplay_w == true) {
                            this.icon_src = require('@/assets/pause.png')
                        }

                    }
                }

            }
        },

        methods: {
            play_pause() {
                this.$emit('play-music', this.music.id)
                if (this.isplay == false) {
                    this.icon_src = require('@/assets/pause.png');
                    this.isplay = true;
                } else {
                    this.icon_src = require('@/assets/play.png')
                    this.isplay = false;
                }
            }
        },

        filters: {
            minutes(value) {
                var seconds = ''
                if ((parseInt(value) % 60) % 10 < 10 && parseInt(value) % 60 < 10) {
                    seconds = '0' + parseInt(value) % 60
                } else {
                    seconds = parseInt(value) % 60
                }

                return parseInt(value / 60) + ":" + seconds;
            }
        }


    }
</script>

<style scoped>
    .item-title {
        display: flex;
        flex-direction: row;
        align-items: center;
    }

    .item-title img {
        margin-right: 20px;
    }

    .music_item {
        margin: 0;
        padding: 0 20px 10px 20px;
        display: flex;
        justify-content: space-between;
        color: white;
        background-color: #505050;
        align-items: center;
    }

    .music_itemon {
        background-color: #424242 !important;
    }

    .music-time {
        justify-content: flex-end
    }

    .title-author {
        font-weight: bold;
    }

</style>