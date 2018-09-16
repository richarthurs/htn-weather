<script>
    import axios from "axios";
    import jquery from "jquery";

    var azure_url = "https://southcentralus.api.cognitive.microsoft.com/customvision/v2.0/Prediction/6dc182f9-bfd8-4500-a0c3-5f78d07c0ab8/url"

    export default {
        mounted() {
            axios({ method: "GET", "url": "https://httpbin.org/ip" }).then(result => {
                this.ip = result.data.origin;
            }, error => {
                console.error(error);
            });
        },
        methods: {
            sendURLData(imgURL) {
                axios({ method: "POST", "url": azure_url, "data": '{"url": imgURL}', "headers": { "content-type":   "application/json",                                                                                                                   "Prediction-Key":  "53465eed449a4f41bfd238b8614cd4af"} }).then(result => {
                    this.response = result.data;
                    console.log(result.data);
                }, error => {
                    console.error(error);
                });
            }
        }
    }
</script>