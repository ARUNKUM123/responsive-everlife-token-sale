<template>
  <v-layout column>
    <v-layout v-bind="binding" wrap class="details-section">
      <v-flex class="pa-2">
        <v-card>
          <v-card-title><h4>Purchased Tokens</h4></v-card-title>
          <v-divider></v-divider>
          <v-list class="text--darken-3 grey--text">
            <v-list-tile>
              <v-list-tile-content class="font-weight-bold text--darken-2 grey--text">{{ user.purchased_ever }}_EVER</v-list-tile-content>
            </v-list-tile>
            
           
          </v-list>
        </v-card>
      </v-flex>
      <v-flex class="pa-2">
        <v-card>
          <v-card-title><h4>Bonus Tokens</h4></v-card-title>
          <v-divider></v-divider>
          <v-list class="text--darken-3 grey--text">
            <v-list-tile>
              <v-list-tile-content class="font-weight-bold text--darken-2 grey--text">{{ user.bonus_ever }} _EVER</v-list-tile-content>
            </v-list-tile>
            
           
          </v-list>
        </v-card>
      </v-flex>
      <v-flex class="pa-2">
        <v-card>
          <v-card-title><h4>Total Tokens</h4></v-card-title>
          <v-divider></v-divider>
          <v-list class="text--darken-3 grey--text">
            <v-list-tile>
              <v-list-tile-content class="font-weight-bold text--darken-2 grey--text">{{ user.total_ever }}_EVER</v-list-tile-content>
            </v-list-tile>
            
           
          </v-list>
        </v-card>
      </v-flex>
      
    </v-layout>
    <v-layout>
        <v-flex class="pa-2">
        <v-card class="boxview" height="418px">
       
          <v-card-title><h4>How it Works</h4></v-card-title>
           <table cellpadding="5"><tr><td style="padding: 10px;padding-bottom: 177px;">
           
           Each token is equivalent to 0.1 USD with estimated crypto conversion listed next to each purchase amount. <BR/> <BR/>Please watch the video to understand how the purchase process works. <BR/>All purchases are subject to a 14 day freeze period. <BR/><BR/> 
           
           
          <button data-v-358c3dbb="" type="button" id="purbtn" class="mt-3 v-btn v-btn--large blue darken-2 white--text" style="position: relative; margin-left: 0px;">
          <div class="v-btn__content">
      <a href="/contribute" style="color: white;padding: 10px; text-decoration: none;">Purchase EVER</a>
      </div></button>

        
            </td><td style="padding: 10px;padding-top: 0px; padding-bottom: 50px; max-width=100%; height: auto !important;"> 
           <iframe width="560" height="315" src="https://www.youtube.com/embed/A2DrqxT5M2c" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe></td></tr>
             </table>
            
           
       
        </v-card>
      </v-flex>
      
    </v-layout>
    <v-layout style=" padding-left: 8px; padding-right: 9px;">
      <payment-table class="mt-5 table" :contributions="user.contributions"></payment-table>
    </v-layout>
  </v-layout>
</template>

<script>
import { mapGetters } from "vuex";
import PaymentTable from "../components/PaymentTable.vue";

export default {
  data() {
    return {};
  },
  computed: {
    ...mapGetters(["user"]),

    binding() {
      const binding = {};
      if (this.$vuetify.breakpoint.mdAndUp) binding.row = true;
      else binding.column = true;
      return binding;
    }
  },
  methods: {
    getKycDetails() {
      if (this.user.kyc) {
        return {
          text: "Verified!",
          color: "green"
        };
      } else if (!this.user.kycDocs.document1) {
        return {
          text: "Documents not submited!",
          color: "red"
        };
      } else if (this.user.kycDocs.document1 && !this.user.kyc) {
        return {
          text: "Verifying!",
          color: "yellow"
        };
      }
    },
    isKycSubmitted() {
      if (this.user.kycDocs.document1) {
        return false;
      } else {
        return true;
      }
    }
  },
  beforeMount() {
    this.$store.dispatch("updateProfile");
  },
  components: {
    PaymentTable
  }
};
</script>
<style scoped>
.table {
  width: 100%;
}

.details-section {
  font-family: "PT Sans", sans-serif;
}
</style>
