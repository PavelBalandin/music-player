<template>
    <div class="container">
        <div class="player">
            <div class="title">
                <span class="title-author">{{music.author}} </span>
                <span class="title-music">{{music.title}}</span>
            </div>

            <input v-on:change="change_current_time" type="range" id="during" name="during"
                   min="0" v-bind:max=music.audio.duration v-model="seek">

            <div class="title-time">
                <span>{{seek | minutes}}</span>
                <span>/</span>
                <span class="music-time">{{music.audio.duration | minutes}}</span>
            </div>

        </div>
        <hr>
    </div>
</template>

<script>
    export default {
        props: ['music', 'seek'],
        name: "Music-info",

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
        },

        methods: {
            change_current_time() {
                this.$emit('change_current_time', this.seek)
            }
        },

    }
</script>

<style scoped>
    .player {
        padding: 0 20px;
        margin: 40px 0 0 0;
        height: 100px;
        background-color: #424242;
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 26px;
    }

    .title {
        width: 30%;
    }

    .title-author {
        font-weight: bold;
        color: white;
    }

    .title-music {
        opacity: 0.9;
        color: white;
    }

    .title-time {
        font-size: 20px;
        opacity: 0.85;
    }

    #during {
        width: 40%;
    }
</style>