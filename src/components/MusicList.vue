<template>
    <div class="container" ref="childComponent">
        <div class="musiclist">
            <div>
                <MusicItem
                        v-for="(music, i) in playlist"
                        v-bind:music="music"
                        v-bind:index="i"
                        v-bind:isplay_w="isplay"
                        v-bind:pre_id="pre_id"
                        v-bind:id="id"

                        v-on:play-music="playmusic"
                />
            </div>
        </div>
        <hr>
    </div>
</template>

<script>
    import MusicItem from '@/components/MusicItem.vue'

    export default {
        props: ['playlist', 'isplay', 'pre_id', 'id'],

        name: "Music-item-list",

        data() {
            return {
                icon_src: require('@/assets/play.png'),
                current: {},
                index: 0,
                previndex: 0,
                bccoloritem: "background: #424242",
            }
        },

        components: {
            MusicItem
        },

        created() {
            this.current = this.playlist[this.index]
        },

        methods: {


            playmusic(id) {
                this.$emit('play-music', id)
            },

        }
    }


</script>

<style scoped>

    .musiclist {
        font-size: 22px;
        background-color: #424242;
        height: 600px;
    }


</style>