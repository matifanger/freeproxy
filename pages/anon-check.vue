<template>
    <div>
        <v-container fluid>
            <v-row>
                <v-col xs="12" sm="12" md="4">
                    <h3 class="text-center mb-5">Your ip-address information</h3>
                        <v-simple-table :loading="mapLoaded" dense>
                        <template v-slot:default>
                            <tbody>
                            <tr>
                                <td>IP-Address</td>
                                <td>{{ipinfo.ip}}</td>
                            </tr>
                             <tr>
                                <td>ISP</td>
                                <td>{{ipinfo.org}}</td>
                            </tr>
                            <tr>
                                <td>Timezone</td>
                                <td>{{ipinfo.timezone}}</td>
                            </tr>
                            <tr>
                                <td>Country</td>
                                <td>{{ipinfo.country_name}}</td>
                            </tr>
                            <tr>
                                <td>City</td>
                                <td>{{ipinfo.city}}</td>
                            </tr>
                            <tr>
                                <td>Latitude</td>
                                <td>{{ipinfo.latitude}}</td>
                            </tr>
                            <tr>
                                <td>Longitude</td>
                                <td>{{ipinfo.longitude}}</td>
                            </tr>
                            </tbody>
                        </template>
                        </v-simple-table>
                </v-col>
                <v-col xs="12" sm="12" md="8">
                    <div id="map"></div>
                </v-col>
                <v-col xs="12" sm="12" md="4" v-if="mapLoaded">
                    <h3 class="text-center pb-5">HTTP Request headers</h3>
                    <template v-for="(value, name) in headers.headers" >
                        {{name}}: {{value}} <br />
                    </template>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>
import axios from "axios";
import mapboxgl from 'mapbox-gl'

    export default {
        data() {
            return {
                ipinfo: [],
                headers: [],

                // MAPBOX
                access_token:'pk.eyJ1IjoiZWltYXR0eiIsImEiOiJja2x0NXJleXUwOTk2Mm9ucWl3NG95ZHFlIn0.6WHPKA6qEsDwsbzzaVz8tQ',
                mapLoaded: false,
                map: {},
                locations: [],
            }
        },
        methods: {
            createMap(){
                mapboxgl.accessToken = this.access_token
                this.map = new mapboxgl.Map({
                    container: 'map',
                    style: 'mapbox://styles/mapbox/streets-v11',
                    zoom: 8,
                    center: this.locations,
                    attributionControl: false
                })
            }
        },
        mounted () {
            // IP ADDRESS INFORMATION
            axios({ method: "GET", "url": "https://httpbin.org/ip" }).then(result => {
                this.ip = result.data.origin;
                axios({ method: "GET", "url": "https://ipapi.co/"+this.ip+"/json/", "data": this.input, "headers": { "content-type": "application/json" } }).then(result => {
                this.ipinfo = result.data;
                this.locations = {lon: this.ipinfo.longitude, lat: this.ipinfo.latitude},
                this.mapLoaded = true
                console.log(this.ipinfo)
                this.createMap()
                }, error => {
                    console.error(error);
                });
            }, error => {
                console.error(error);
            });
            // HEADERS
            axios({ method: "GET", "url": "https://httpbin.org/headers", "data": this.input, "headers": { "content-type": "application/json" } }).then(result => {
                this.headers = result.data;
                console.log(this.headers)
                }, error => {
                    console.error(error);
                })
            
    },
    }
</script>

<style lang="scss" scoped>
#map {   width:100%;   height:40vh;}
</style>