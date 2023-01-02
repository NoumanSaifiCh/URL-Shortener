<template >
  <v-container fluid>
    <v-row class="text-center black">
      <v-card class=" d-flex justify-center flex-sm-row flex-colum black" height="auto" width="100%" flat>
        <v-app-bar dark prominent flat min-height="135px" class="black">
          <v-card-text>
            <h1>Paste the URL to be shortened</h1>
            <v-row class="d-flex justify-center my-1">
              <v-col cols="7" sm="6">
                <v-text-field v-model="longUrl" color="white" outlined label="write the url"></v-text-field>
              </v-col>
              <v-btn class="mt-5" depressed color="grey darken-1" @click="HandleSubmit" elevation="15">
                Submit
              </v-btn>
            </v-row>
          </v-card-text>
        </v-app-bar>
      </v-card>
    </v-row>
    <v-row class="text-center black ">
      <v-card class="black " width="100%">
        <v-card-text v-show="shortUrl">
          <div>
            <p class="white--text font-weight-bold text-lg-subtitle-1"> <span class="mr-4">Short URL: </span>{{ shortUrl
              }}</p>
          </div>
        </v-card-text>
      </v-card>
    </v-row>
    <v-container fluid>
      <div class="mt-3 d-flex justify-center flex-sm-row flex-column" color='grey darken-3'>
        <v-card class="pa-2" flat height="">
          <v-list-item three-line class="">
            <v-list-item-content class="ma-3">
              <v-icon color="yellow" size="50px">
                mdi-thumb-up
              </v-icon>
              <v-list-item-title class="text-h5 mb-1 text-center">
                Easy
              </v-list-item-title>
              <v-list-item-subtitle class="text-center">Url Shortener is easy and fast and effective way to shorten your
                long urls</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-card>

        <v-card class="pa-2" flat height="">
          <v-list-item three-line class="d-flex justify-center ma-3">
            <v-list-item-content class="d-flex justify-center  ma-3">
              <v-icon color="blue-grey darken-1" size="50px">
                mdi-link-variant
              </v-icon>
              <v-list-item-title class="text-h5 mb-1 text-center">
                Shortened
              </v-list-item-title>
              <v-list-item-subtitle class="text-center">Any links can be shortener with our powerful
                algorithms</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-card>

        <v-card class="pa-2" flat height="">
          <v-list-item three-line class="d-flex justify-center ma-3">
            <v-list-item-content class="d-flex justify-center  ma-3">
              <v-icon color="yellow" size="50px">
                mdi-lock-check-outline
              </v-icon>
              <v-list-item-title class="text-h5 mb-1 text-center">
                Secure
              </v-list-item-title>
              <v-list-item-subtitle class="text-center">With high level encryption your urls are always safe and secure
                with https</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-card>
      </div>
    </v-container>

    <v-container fluid>
      <div class="mt-1 d-flex justify-center flex-sm-row flex-column" color='grey darken-3'>
        <v-card class="pa-1" flat height="">
          <v-list-item three-line class="d-flex justify-center ">
            <v-list-item-content class="d-flex justify-center  ma-3">
              <v-icon color="green" size="50px">
                mdi-signal
              </v-icon>
              <v-list-item-title class="text-h5 mb-1 text-center">
                Statistics
              </v-list-item-title>
              <v-list-item-subtitle class="text-center">You can see stats on how many users have used your shortened
                url</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-card>

        <v-card class="pa-1" flat height="">
          <v-list-item three-line class="d-flex justify-center ">
            <v-list-item-content class="d-flex justify-center  ma-3">
              <v-icon color="deep-purple lighten-2" size="50px">
                mdi-cog-refresh-outline
              </v-icon>
              <v-list-item-title class="text-h5 mb-1 text-center">
                Reliable
              </v-list-item-title>
              <v-list-item-subtitle class="text-center">We delete any links which is a potential threat to malware or
                viruses </v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-card>

        <v-card class="pa-1" flat height="">
          <v-list-item three-line class="d-flex justify-center ">
            <v-list-item-content class="d-flex justify-center  ma-3">
              <v-icon color="teal darken-2" size="50px">
                mdi-monitor-cellphone-star
              </v-icon>
              <v-list-item-title class="text-h5 mb-1 text-center">
                Devices
              </v-list-item-title>
              <v-list-item-subtitle class="text-center">Compatible with smartphones, tablets and
                desktop</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-card>
      </div>
    </v-container>

  </v-container>
</template>
  
<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      longUrl: "",
      shortUrl: "",
    }
  },

  methods: {

    HandleSubmit() {
      const url = new URL(
        "https://t.ly/api/v1/link/shorten"
      );

      const params = {
        "api_token": "Dt6GxJgv3IVhySbmQEEgErHa6YW5Bnvc0rG2FLt0Xon437nhHE0AtSr2a3Vd",
      };
      Object.keys(params)
        .forEach(key => url.searchParams.append(key, params[key]));

      const headers = {
        "Content-Type": "application/json",
        "Accept": "application/json",
      };

      let body = {
        "long_url": this.longUrl,
        "domain": "https://t.ly/",
        "include_qr_code": false
      };

      fetch(url, {
        method: "POST",
        headers,
        body: JSON.stringify(body),
      }).then(response => response.json())
        .then((data) => { this.shortUrl = data.short_url })

    }
  }

}
</script>
  