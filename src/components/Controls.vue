<template>
    <div class="container">
        <div class="component">
            <div class="play-point">
                <div><img v-on:click="$emit('previous_track')" id="prev" src="@/assets/next.png" alt="Previoos"></div>
                <div><img @click="play_pause" v-bind:src=icon_src alt="Start"></div>
                <div><img v-on:click="$emit('next_track')" src="@/assets/next.png" alt="Next"></div>
            </div>
            <div class="play-point">
                <input v-on:change="change_volume" type="range" id="volume" name="volume" min="0" max="100"
                       v-model="volume">
                <div id="volume_counter">{{volume}}</div>
                <div><img v-on:click="mute" v-bind:src=icon_src_mute alt=""></div>
            </div>
        </div>
        <hr>
    </div>
</template>

<script>
    export default {
        name: "Music-controls",
        props: ['isplay'],

        data() {
            return {
                music: new Audio(require('@/audio/Warriyo - Mortals.mp3')),
                icon_src: require('@/assets/play.png'),
                icon_src_mute: require('@/assets/volumeon.png'),
                //isplay: false,
                volume: 50,
                pre_volume: 50
            }
        },

        watch: {
            isplay() {
                if (this.isplay == false) {
                    this.icon_src = require('@/assets/play.png');
                } else {
                    this.icon_src = require('@/assets/pause.png');
                }
            }
        },

        methods: {

            play_pause() {
                if (this.isplay == false) {
                    this.$emit('play-pause');
                    this.icon_src = require('@/assets/pause.png');
                    // this.isplay = true;
                } else {
                    this.$emit('play-pause');
                    this.icon_src = require('@/assets/play.png');
                    // this.isplay = false;
                }
            },
            change_volume() {
                this.$emit('change-volume', this.volume)
                if (this.volume == 0) {
                    this.icon_src_mute = require('@/assets/volumeof.png');
                } else {
                    this.icon_src_mute = require('@/assets/volumeon.png');
                }
            },


            mute() {
                if (this.volume != 0) {
                    this.$emit('change-volume', 0);
                    this.pre_volume = this.volume;
                    this.volume = 0;
                    this.icon_src_mute = require('@/assets/volumeof.png');
                } else {
                    this.$emit('change-volume', this.pre_volume)
                    this.volume = this.pre_volume;
                    this.icon_src_mute = require('@/assets/volumeon.png');
                }
            }
        }
    }
</script>

<style scoped>
    .component {
        height: 100px;
        background-color: #212121;
        padding: 0 20px;
        margin: 0;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .component img {
        margin-left: 10px;
        margin-right: 10px;

    }

    .play-point {
        display: flex;
        flex-direction: row;
        align-items: center;
    }

    #volume_counter {
        width: 20px;
        padding: 0 5px;
    }

    #volume {
        width: 200px;
    }

    #prev {
        transform: rotate(180deg);
    }
</style>