<template>
    <div class="hello">
        <input type="text" v-model="input.firstname" placeholder="First Name" />
        <button v-on:click="sendData()">Send</button>
        <br />
        <br />
        <textarea>{{ response }}</textarea>
    </div>
</template>

<script>
    import axios from "axios";
    import jquery from "jquery";

    var azure_url = "https://" + "westcentralus" + ".api.cognitive.microsoft.com/vision/" + "v1.0/analyze" + "?" + "visualFeatures=Categories%2CDescription%2CColor&details=&language=en"

    export default {
        name: 'HelloWorld',
        data () {
            return {
                ip: "",
                input: {
                    firstname: "",
                },
                response: ""
            }
        },
        mounted() {
            axios({ method: "GET", "url": "https://httpbin.org/ip" }).then(result => {
                this.ip = result.data.origin;
            }, error => {
                console.error(error);
            });
        },
        methods: {
            sendData() {
                axios({ method: "POST", "url": azure_url, "data": '{"url": "https://hdrexposed.zenfolio.com/img/s/v-3/p919518288-3.jpg"}', "headers": { "content-type":   "application/json",
                                                                                                                                    "Ocp-Apim-Subscription-Key":  "b11c9fd600af44ac9a47523923a7fd17"} }).then(result => {
                    this.response = result.data;
                    console.log(result.data);
                }, error => {
                    console.error(error);
                });
            }
        }
    }
</script>

<style scoped>
    h1, h2 {
        font-weight: normal;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }

    textarea {
        width: 600px;
        height: 200px;
    }
</style>