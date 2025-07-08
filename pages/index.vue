<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <template>
  <v-data-table
    :headers="headers"
    :items="customers"
    :items-per-page="10"
    class="elevation-1"
    :loading="loading"
    loading-text="loading please wait"
  >
  
<template v-slot:item.profilePicture="{item}">
   <v-badge
          color="green"
          content="VIP"
          offset-y="60"
          v-if="item.isVip == true"
        >

        
  <v-img
  lazy-src="https://picsum.photos/id/11/10/6"
  max-height="200"
  max-width="100"
  :src="item.profilePicture"
></v-img></v-badge>
<div v-else><v-img
  lazy-src="https://picsum.photos/id/11/10/6"
  max-height="200"
  max-width="100"
  :src="item.profilePicture"
></v-img></div>
</template>
<template v-slot:item.actions="{item}">
  <v-btn color="primary" @click="getCustomerDetails(item)">view</v-btn>
</template>
</v-data-table>
<template>
  <!-- dialog -->
  <div class="text-center">
    <v-dialog
      v-model="dialog"
      width="500"
    >
      <v-card>
        <v-card-title class="primary">
          Privacy Policy
        </v-card-title>
   <v-row >
    <v-col cols="12" md="4">
      <v-img
          lazy-src="https://picsum.photos/id/11/10/6"
          max-height="150"
          max-width="250"
          src="https://picsum.photos/id/11/500/300"
></v-img>
    </v-col>
    <v-col cols="12" md="8">
      <v-list-item>
      <v-list-item-content>
        <v-list-item-title>Single-line item</v-list-item-title>
      </v-list-item-content>
    </v-list-item>

    <v-list-item two-line>
      <v-list-item-content>
        <v-list-item-title>Two-line item</v-list-item-title>
        <v-list-item-subtitle>Secondary text</v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

    <v-list-item three-line>
      <v-list-item-content>
        <v-list-item-title>Three-line item</v-list-item-title>
        <v-list-item-subtitle>
          Secondary line text Lorem ipsum dolor sit amet,
        </v-list-item-subtitle>
        <v-list-item-subtitle>
          consectetur adipiscing elit.
        </v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>
    </v-col>
   </v-row>
        

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="dialog = false"
          >
            I accept
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
</template>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  data(){
    return{
      headers: [
        
          // {
          //   text: 'ID',
          //   align: 'start',
          //   sortable: false,
          //   value: 'id',
          // },
          { text: 'Photo', value: 'profilePicture' },
          { text: 'Name', value: 'name' },
          { text: 'Email', value: 'email' },
          { text: 'Phone', value: 'phone' },
          { text: 'Address', value: 'address' },
          { text: 'Status', value: 'isVip' },
          { text: '', value: 'actions' },
        ],
        customers:[],
        loading:true,
        dialog: false,
        customerName: "",
        customerEmail: "",
        customerPhone: "",
        customerAge: 0
        
    }
  },
 
  methods:{
    getCustomers(){
      this.$axios.get('/customers')
      .then(response =>{
        console.log(response.data)
        this.customers = response.data
        this.loading = false
      })
      .catch(err =>{
        console.log(err)
      })
    },
    getCustomerDetails(item){
      console.log(item),
      this.dialog = true
    }
  },
  mounted(){
    this.getCustomers()
  }
}
</script>
