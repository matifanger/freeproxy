<template>
    <div>

<v-container fluid>
  <v-row>
    <v-col cols="12"><h1 align="center"> <v-icon x-large color="black" class="mt-n2">mdi-database</v-icon>PROXYDB stats</h1></v-col>
    
    <v-col class="d-flex flex-wrap justify-center" align="center">
      
      <v-card width="15em" height="8em" id="red" class="ml-5" :class="{'mb-4': $vuetify.breakpoint.mdAndDown}"><p style="color:white; font-size:35px" class="pt-3 ml-3 mr-3">1564<br/>Transparent</p></v-card>
      <v-card width="15em" height="8em" id="black" class="ml-5" :class="{'mb-4': $vuetify.breakpoint.mdAndDown}"><p style="color:white; font-size:35px" class="pt-3 ml-3 mr-3">3545<br/>Anonymous</p></v-card>
      <v-card width="15em" height="8em" id="blue" class="ml-5" :class="{'mb-4': $vuetify.breakpoint.mdAndDown}"><p style="color:white; font-size:35px" class="pt-3 ml-3 mr-3">5314<br/>Distorting</p></v-card>
      <v-card width="15em" height="8em" id="green" class="ml-5" :class="{'mb-4': $vuetify.breakpoint.mdAndDown}"><p style="color:white; font-size:35px" class="pt-3 ml-3 mr-3">12954<br/>Elite</p></v-card>
    </v-col>

    <v-col cols="12" align="center">
      <v-btn x-large 
      href="https://firebasestorage.googleapis.com/v0/b/free-proxy-40e6d.appspot.com/o/proxies_list.json?alt=media&token=02ee8456-b657-462a-82d8-18ef1141f2e4" 
      download class="mt-10" color="primary">Download all proxies<v-icon right>mdi-download</v-icon>
      </v-btn>
      
    </v-col>

  </v-row>
</v-container>

    </div>
</template>

<script>
    export default {
    data() {
      return {
        }
    },
    methods: {

    },
  }
</script>

<style lang="scss" scoped>
#red {
  background: rgba(0, 0, 0, 0) linear-gradient(to right, rgb(255, 118, 87), rgb(227, 74, 74)) repeat scroll 0% 0%;
}

#black {
  background: rgba(0, 0, 0, 0) linear-gradient(to right, rgb(99, 96, 95), rgb(0, 0, 0)) repeat scroll 0% 0%;
}

 #blue {
   background: rgba(0, 0, 0, 0) linear-gradient(to right, rgb(52, 181, 229), rgb(46, 132, 224)) repeat scroll 0% 0%;
 }

 #green {
   background: rgba(0, 0, 0, 0) linear-gradient(to right, rgb(102, 229, 181), rgb(41, 224, 105)) repeat scroll 0% 0%;
 }
</style>