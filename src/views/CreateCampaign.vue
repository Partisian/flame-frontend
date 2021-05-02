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
  <div class="form-group">
   <v-form>
    <v-container>
      <v-row>
        <v-col
          cols="12"
          sm="6"
        >
          <v-text-field
            v-model="campaignname"
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
        ref="menu"
        v-model="menu"
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
          v-model="date"
          no-title
          scrollable
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="menu = false"
          >
            Cancel
          </v-btn>
          <v-btn
            text
            color="primary"
            @click="$refs.menu.save(date)"
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
        ref="menu"
        v-model="menu"
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
          v-model="date"
          no-title
          scrollable
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="menu = false"
          >
            Cancel
          </v-btn>
          <v-btn
            text
            color="primary"
            @click="$refs.menu.save(date)"
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
            v-model="mediadescription"
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
export default{
  name:'',
  data(){
    return{
        campaignname: 'Nike',
        datefrom: new Date().toISOString().substr(0, 10),
        dateto: new Date().toISOString().substr(0, 10),
        menu: false,
        mediadescription: 'Description of the Campaign',
        addtnmediadesc: 'Additional description of the Campaign',
        contact: '12345678',
        category: ['Sports', 'Food', 'Fashion', 'Jewelry'],
        reward: '12345678',
    }
  },
  methods:{
  }
}
</script>

<style scoped>
</style>
