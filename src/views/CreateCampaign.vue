<template>
  <div class="createcampaign mt-8">
<div class="pa-4 primary text-no-wrap rounded-lg ma-5">
<v-row>
  <v-col
    cols="12"
    sm="6"
  >
  <span class="white--text">Create Campaign</span>
  </v-col>
</v-row>
</div>
<transition name="fade" mode="out-in">
  <div v-if="createCampaignClicked" class="alert alert-success" role="alert" >
   <v-alert
      dense
      text
      type="success"
      display=false
    >
      The campaign <strong>{{campaignTitle}}</strong> has been created <strong>successfully</strong>
    </v-alert>
  </div>
  </transition>
  <div class="form-group">
   <v-form >
    <v-container>
      <v-row>
        <v-col
          cols="12"
          sm="6"
        >
          <v-text-field
            v-model="campaignTitle"
            label="Campaign Name"
            clearable
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-file-input
        accept="image/*"
        label="File input"
        ></v-file-input>
      </v-row>
  <v-row>
    <v-col
      cols="12"
      sm="6"
      md="4"
    >
      <v-menu
        ref="datefrommenu"
        v-model="datefrommenu"
        :close-on-content-click="false"
        :return-value.sync="date"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="datefrom"
            label="Start Date"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="datefrom"
          no-title
          scrollable
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="datefrommenu = false"
          >
            Cancel
          </v-btn>
          <v-btn
            text
            color="primary"
            @click="$refs.datefrommenu.save(datefrom)"
          >
            OK
          </v-btn>
        </v-date-picker>
      </v-menu>
    </v-col>
    <v-col
      cols="12"
      sm="6"
      md="4"
    >
      <v-menu
        ref="datetomenu"
        v-model="datetomenu"
        :close-on-content-click="false"
        :return-value.sync="date"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="dateto"
            label="End Date"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="dateto"
          no-title
          scrollable
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="datetomenu = false"
          >
            Cancel
          </v-btn>
          <v-btn
            text
            color="primary"
            @click="$refs.datetomenu.save(dateto)"
          >
            OK
          </v-btn>
        </v-date-picker>
      </v-menu>
    </v-col>
  </v-row>
      <v-row>
        <v-col
          cols="12"
        >
          <v-text-field
            v-model="campaignDesc"
            label="Media Description"
            clearable
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col
          cols="12"
        >
          <v-text-field
            v-model="addtnmediadesc"
            label="Additional Media Description"
            clearable
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col
          cols="12"
          sm="4"
        >
          <v-text-field
            v-model="contact"
            label="Contact Number"
            clearable
          ></v-text-field>
        </v-col>
        <v-col
          cols="12"
          sm="4"
        >
          <v-select
            :items="category"
            label="Category"
            outlined
          ></v-select>
        </v-col>
        <v-col
          cols="12"
          sm="4"
        >
          <v-text-field
            v-model="reward"
            label="Reward (SGD)"
            clearable
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
    <v-btn
      depressed
      color="primary"
      @click.prevent="createCampaign()"
    >
      Create Campaign
    </v-btn>
      </v-row>
    </v-container>
  </v-form>
  </div>

  </div>
</template>

<script>
const baseUrl = 'http://localhost:8081/';
import User from '../models/user';
import axios from 'axios'
export default{
  name: 'CreateCampaign',
  data: function() {
    return{
        user: [],
        createCampaignClicked: false,
        date:'',
        brandId:'',
        datetomenu:'',
        datefrommenu:'',
        campaignTitle: 'Nike',
        datefrom: '',
        dateto: '',
        //dateto: new Date().toISOString().substr(0, 10),
        menu: false,
        campaignDesc: 'Description of the Campaign',
        addtnmediadesc: 'Additional description of the Campaign',
        contact: '12345678',
        category: ['Sports', 'Food', 'Fashion', 'Jewelry'],
        reward: '12345678',
    }
  },
  computed: {
    currentUser() {
      return this.$store.state.auth.user;
    }
  },
  methods:{
    createCampaign(){
      this.url = baseUrl + 'api/v1/campaign/';
      const campaigndata = {
      brandId:this.$store.state.auth.user.id,
      campaignTitle:this.campaignTitle,
      campaignDesc:this.campaignDesc,
      campaignCreateDate:new Date().toISOString().substr(0, 10),
      campaignStatus:'0'
      };
      axios.post(this.url,campaigndata).then(resp => {
      console.log(`HTTP Response: ${resp.status}, ${resp.statusText}`);
      console.log(`Response Data: ${resp.data.length} items`);
      this.createCampaignClicked=true;
      }).catch(error => {
        console.log(error)
        this.errored = true
      })
       //alert('Submitted')
      //this.$axios.post('http://18.138.248.19:8080/api/campaign',{
      //  campaignTitle: this.campaignTitle,
      //  brandId:'4',
      //  campaignDesc:this.mediadescription,
      //  campaignCreateDate:new Date().toISOString().substr(0, 10),
      //  campaignStatus:'0'
      //}).then((response)=>{this.console.log(response)}).catch((error)=>{this.console.log(error)})
      
      /*axios.post('http://18.138.248.19:8080/api/campaign', {
        campaignTitle: this.campaignTitle,
        brandId:'4',
        campaignDesc:this.mediadescription,
        campaignCreateDate:new Date().toISOString().substr(0, 10),
        campaignStatus:'0'
      })
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      });*/

    }
  },
  watch:{
    createCampaignClicked(val){
      if (val){
        setTimeout(()=>this.createCampaignClicked=false,1000);
      }
    }
  }
}
</script>

<style scoped>
</style>
