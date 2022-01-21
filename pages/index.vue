<template>
<v-container fluid class="pa-0">
  <v-row class="">
    <v-col xs="2" sm="3" md="2" class="">
      <h3>Protocols</h3>
      <v-radio-group v-model="protocol">
      <v-radio value="All" label="All"/>
      <v-radio value="HTTP" label="HTTP"/>
      <v-radio value="HTTPS" label="HTTPS"/>
      <v-radio value="SOCKS4" label="SOCKS4"/>
      <v-radio value="SOCKS5" label="SOCKS5"/>
    </v-radio-group>
  </v-col>
  <v-col xs="2" sm="3" md="2" class="">
    <h3>Anonymity level</h3>
      <v-radio-group v-model="anonymity">
      <v-radio value="All" label="All"/>
      <v-radio value="Transparent" label="Transparent"/>
      <v-radio value="Anonymous" label="Anonymous"/>
      <v-radio value="Distorting" label="Distorting"/>
      <v-radio value="Elite" >
                <template v-slot:label>
          <strong class="green--text">Elite</strong>
        </template>
      </v-radio>
    </v-radio-group>
  </v-col>
    <v-col xs="2" sm="3" md="4" class="">
      <h3 :class="{'mt-n9': $vuetify.breakpoint.xs}">Country</h3>
      <v-combobox class="mt-5" v-model="countrySelected" :items="getCountriesName()" outlined placeholder="- All Countries -" label="Country"></v-combobox>
      <v-row justify="center" align="center" class="">
      <v-btn  v-on:click="getDB()" class="mr-3">Search<v-icon right>mdi-magnify</v-icon></v-btn>
      <v-btn href="https://firebasestorage.googleapis.com/v0/b/free-proxy-40e6d.appspot.com/o/proxies_list.json?alt=media&token=02ee8456-b657-462a-82d8-18ef1141f2e4" download :class="{'mt-2': $vuetify.breakpoint.md}" color="primary">Download all proxies<v-icon right>mdi-download</v-icon></v-btn>
      </v-row>
  </v-col>
</v-row>

<v-row>
<v-col>
  <v-data-table
    :headers="headers"
    :items="content"
    class="elevation-1"
  >
    <template v-slot:item.anonymity="{ item }">
      <v-chip
        :color="getColor(item.anonymity)"
        dark
      >
        {{ item.anonymity }}
      </v-chip>
    </template>

    <template v-slot:item.country="{ item }">  
      <div class="d-inline">
  <gb-flag class="pt-1" :code="item.country" size="small"></gb-flag>
  <div class="d-inline pl-1 pt-n2">{{item.country}}</div> </div>
    </template>

        <template v-slot:item.uptime="{ item }">
      <v-chip
        :color="getUptimeColor(item.uptime)"
        dark
      >
        {{ item.uptime }}
      </v-chip>
    </template>

  </v-data-table>
    </v-col>
  </v-row>
</v-container>
</template>

<script>

export default {
  data() {
    return {
      countrySelected: '- All countries -',
      countries: [],
      protocol: 'All',
      anonymity: 'All',
        headers: [
          {
            text: 'IP',
            align: 'start',
            sortable: false,
            value: 'ip',
          },
          { text: 'Country', value: 'country' },
          { text: 'Anonymity', value: 'anonymity' },
          { text: 'Protocol', value: 'protocol' },
          { text: 'Uptime %', value: 'uptime' },
          { text: 'RTime', value: 'rtime' },
          { text: 'Checked Ago', value: 'checkedAgo' },
        ],
        content: [],
    }
    },
    mounted() {

      // get proxies
      this.$fire.firestore.collection("content").limit(15).get().then((querySnapshot) => {
          querySnapshot.forEach( (doc) => {
              console.log(doc.id, " => ", doc.data());
              this.content.push(doc.data())}
              );
      })
      .catch(function(error) {
          console.log("Error getting documents: ", error);
      });
      
      // Get countries
      this.$fire.firestore.collection("countries").get().then((querySnapshot) => { querySnapshot.forEach( (doc) => {
              console.log(doc.id, " => ", doc.data());
              this.countries.push(doc.data())
              }
              );
          })
          .catch(function(error) {
          console.log("Error getting documents: ", error);
      });

    },
    methods: {
      getColor (anonymity) {
        if (anonymity == 'Transparent') return 'red'
        else if (anonymity == 'Anonymous') return 'black'
        else if (anonymity == 'Distorting') return 'primary'
        else if (anonymity == 'Elite') return 'green'
      },
      getUptimeColor (uptime) {
        if (uptime[0] <= '6') return 'red'
        else if (uptime[0] == '7') return 'orange'
        else if (uptime[0] == '8') return 'light-green'
        else if (uptime[0] == '9') return 'green'
      },
      getCountriesName() {
        let countriesReturned = ['- All Countries -'];
        for (var item in this.countries) {
          if (this.countries[item].ammount_proxies > 0) {
          countriesReturned.push(this.countries[item].code)
          }
        }
        return countriesReturned
      },
      getDB(){
            // this.$fire.firestore.collection("content").doc()
            var query = this.$fire.firestore.collection("content")
            if (this.countrySelected != '- All Countries -') {
            query = query.where("country", "==", this.countrySelected)
            }
            if (this.anonymity != 'All') {
            query = query.where("anonymity", "==", this.anonymity)
            }
            if (this.protocol != 'All') {
            query = query.where("protocol", "==", this.protocol)
            }
            
            query.limit(100).get()
            .then((querySnapshot) => {
              this.content = []
                querySnapshot.forEach( (doc) => {
                    // doc.data() is never undefined for query doc snapshots
                    console.log(doc.id, " => ", doc.data());
                    this.content.push(doc.data())
                }
                );
            })
            .catch(function(error) {
                console.log("Error getting documents: ", error);
            });

        },
    },
  }
</script>
