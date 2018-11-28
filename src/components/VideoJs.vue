<template>
    <div>
        <video id="rbc" class="video-js vjs-default-skin" controls preload="auto" width="640" height="360" data-setup='{}'>
            <source :src="video" type="video/mp4">
        </video>
    </div>
</template>

<script>
    export default {
        name: "VideoJs",
        props: ['video', 'vast'],
        mounted() {
            this.player = videojs('rbc');
            if (this.vast) {
                this.player.ima({
                    id: 'rbc',
                    adTagUrl: this.vast
                })
            }
        },
        beforeDestroy() {
            if (this.player) {
                this.player.dispose();
            }
        },
        data() {
            return {
                src: null
            }
        },
        updated() {
            console.log("HAHA");
        },
        methods: {
            update() {



            }
        }
    }
</script>

<style scoped>

</style>
