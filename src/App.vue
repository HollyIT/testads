<template>
    <div id="app">
        <div class="video">
            <video-js v-if="loaded" :video="video" :vast="vast" ref="video"></video-js>
        </div>
        <div class="form">
            <div class="form-group">
                <label for="vastUrl">VAST URL</label>
                <input type="url" class="form-control" id="vastUrl" v-model="vast" placeholder="Enter URL to Vast feed">
            </div>
            <ul>
                <li v-for="(sample, name) in samples">
                    <a href="#" @click.prevent="setAd(sample)" v-text="name"></a>
                </li>
            </ul>
            <div class="form-group">
                <label for="videoUrl">Video URL</label>
                <input type="url" class="form-control" id="videoUrl" v-model="video" placeholder="Enter URL to video">
            </div>
            <button class="btn btn-primary" @click="update">Update</button>
        </div>
    </div>
</template>

<script>

    import VideoJs from "./components/VideoJs";

    export default {
        name: 'app',
        components: {
            VideoJs
        },

        data() {
            let samples = {
                'regular': 'http://pubads.g.doubleclick.net/gampad/ads?sz=640x480&iu=/124319096/external/ad_rule_samples&ciu_szs=300x250&ad_rule=1&impl=s&gdfp_req=1&env=vp&output=xml_vmap1&unviewed_position_start=1&cust_params=sample_ar%3Dpremidpostpod%26deployment%3Dgmf-js&cmsid=496&vid=short_onecue&correlator=',
                'skip': 'https://pubads.g.doubleclick.net/gampad/ads?sz=640x480&iu=/124319096/external/single_ad_samples&ciu_szs=300x250&impl=s&gdfp_req=1&env=vp&output=vast&unviewed_position_start=1&cust_params=deployment%3Ddevsite%26sample_ct%3Dskippablelinear&correlator=',
                'nonlinear': 'https://pubads.g.doubleclick.net/gampad/ads?sz=480x70&iu=/124319096/external/single_ad_samples&ciu_szs=300x250&impl=s&gdfp_req=1&env=vp&output=vast&unviewed_position_start=1&cust_params=deployment%3Ddevsite%26sample_ct%3Dnonlinear&correlator=',
                'preroll+bumper': 'https://pubads.g.doubleclick.net/gampad/ads?sz=640x480&iu=/124319096/external/ad_rule_samples&ciu_szs=300x250&ad_rule=1&impl=s&gdfp_req=1&env=vp&output=vmap&unviewed_position_start=1&cust_params=deployment%3Ddevsite%26sample_ar%3Dpreonlybumper&cmsid=496&vid=short_onecue&correlator=',

            };
            return {
                vast: 'http://pubads.g.doubleclick.net/gampad/ads?sz=640x480&iu=/124319096/external/ad_rule_samples&ciu_szs=300x250&ad_rule=1&impl=s&gdfp_req=1&env=vp&output=xml_vmap1&unviewed_position_start=1&cust_params=sample_ar%3Dpremidpostpod%26deployment%3Dgmf-js&cmsid=496&vid=short_onecue&correlator=',
                video: 'https://media.crooksandliars.com/2018/11/40775.mp4_high.mp4',
                samples: samples,
                loaded: true
            }
        },

        methods: {
            update() {
                this.loaded = false;
                this.$nextTick(() => {
                    this.loaded = true;
                })
            },

            setAd(url) {
                this.vast = url;
                this.$nextTick(()=> {
                    this.update();
                })

            }
        }
    }
</script>

<style lang="scss">
    @import '~video.js/dist/video-js.css';
    @import '~bootstrap/scss/bootstrap';
    @import '~videojs-contrib-ads/dist/videojs-contrib-ads.css';
    @import '~videojs-ima/dist/videojs.ima.css';

    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;

    }

    body {
        margin: 20px;

    }
</style>
