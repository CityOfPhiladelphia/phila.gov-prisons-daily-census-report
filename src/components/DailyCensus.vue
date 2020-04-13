<template>
  <div>
    <div v-show="loading" class="mtm center">
      <i class="fas fa-spinner fa-spin fa-3x" />
    </div>
    <div v-show="!loading && empty" class="h3 mtm center">Sorry, there are no results.</div>
    <div v-show="failure" class="h3 mtm center">Sorry, there was a problem. Please try again.</div>
    <table v-show="!empty && !loading && !failure">
      <caption>Daily census report for {{ censusData.date }}</caption>
      <thead>
        <tr>
          <td></td>
          <th colspan="4"></th>
          <th colspan="8"> Not in facility</th>
         
          <td></td>
        </tr>
        <tr>
          <td></td>
          <th colspan="2">Adult</th>
          <th colspan="2">Juvenile</th>
          <th colspan="2">Workers</th>
          <th colspan="2">Furlough</th>
          <th colspan="2">Open ward</th>
          <th colspan="2">Emergency trips</th>
          <td></td>
        </tr>
        <tr>
          <th scope="col">Facility</th>
          <th scope="col">Male</th>
          <th scope="col">Female</th>
          <th scope="col">Male</th>
          <th scope="col">Female</th>
          <th scope="col">Male</th>
          <th scope="col">Female</th>
          <th scope="col">Male</th>
          <th scope="col">Female</th>
          <th scope="col">Male</th>
          <th scope="col">Female</th>
          <th scope="col">Male</th>
          <th scope="col">Female</th>
          <th scope="col">Total</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th scope="row">Riverside Correctional Facility Alternative and Special Detention Central Unit</th>
          <td>{{ censusData.asdcuMale }}</td>
          <td>{{ censusData.asdcuFemale }}</td>
          <td>{{ censusData.asdcuMaleJuv }}</td>
          <td>{{ censusData.asdcuFemaleJuv }}</td>
          <td>{{ censusData.asdcuNifWorkerMale }}</td>
          <td>{{ censusData.asdcuNifWorkerFemale }}</td>
          <td>{{ censusData.asdcuNifFurMale }}</td>
          <td>{{ censusData.asdcuNifFurFemale }}</td>
          <td>{{ censusData.asdcuNifOwMale }}</td>
          <td>{{ censusData.asdcuNifOwFemale }}</td>
          <td>{{ censusData.asdcuNifEtMale }}</td>
          <td>{{ censusData.asdcuNifEtFemale }}</td>
          <td>{{ censusData.asdcuTotal }}</td>
        </tr>
        <tr>
          <th scope="row">Curran-Fromhold Correctional Facility</th>
          <td>{{ censusData.cfcfMale }}</td>
          <td>{{ censusData.cfcfFemale }}</td>
          <td>{{ censusData.cfcfMaleJuv }}</td>
          <td>{{ censusData.cfcfFemaleJuv }}</td>
          <td>{{ censusData.cfcfNifWorkerMale }}</td>
          <td>{{ censusData.cfcfNifWorkerFemale }}</td>
          <td>{{ censusData.cfcfNifFurMale }}</td>
          <td>{{ censusData.cfcfNifFurFemale }}</td>
          <td>{{ censusData.cfcfNifOwMale }}</td>
          <td>{{ censusData.cfcfNifOwFemale }}</td>
          <td>{{ censusData.cfcfNifEtMale }}</td>
          <td>{{ censusData.cfcfNifEtFemale }}</td>
          <td>{{ censusData.cfcfTotal }}</td>
        </tr>
        <tr>
          <th scope="row">Detention Center</th>
          <td>{{ censusData.dcMale }}</td>
          <td>{{ censusData.dcFemale }}</td>
          <td>{{ censusData.dcMaleJuv }}</td>
          <td>{{ censusData.dcFemaleJuv }}</td>
          <td>{{ censusData.dcNifWorkerMale }}</td>
          <td>{{ censusData.dcNifWorkerFemale }}</td>
          <td>{{ censusData.dcNifFurMale }}</td>
          <td>{{ censusData.dcNifFurFemale }}</td>
          <td>{{ censusData.dcNifOwMale }}</td>
          <td>{{ censusData.dcNifOwFemale }}</td>
          <td>{{ censusData.dcNifEtMale }}</td>
          <td>{{ censusData.dcNifEtFemale }}</td>
          <td>{{ censusData.dcTotal }}</td>
        </tr>
        <tr>
          <th scope="row">Detention Center Public Health Services Wing</th>
          <td>{{ censusData.dcPhswMale }}</td>
          <td>{{ censusData.dcPhswFemale }}</td>
          <td>{{ censusData.dcPhswMaleJuv }}</td>
          <td>{{ censusData.dcPhswFemaleJuv }}</td>
          <td>{{ censusData.dcPhswNifWorkerMale }}</td>
          <td>{{ censusData.dcPhswNifWorkerFemale }}</td>
          <td>{{ censusData.dcPhswNifFurMale }}</td>
          <td>{{ censusData.dcPhswNifFurFemale }}</td>
          <td>{{ censusData.dcPhswNifOwMale }}</td>
          <td>{{ censusData.dcPhswNifOwFemale }}</td>
          <td>{{ censusData.dcPhswNifEtMale }}</td>
          <td>{{ censusData.dcPhswNifEtFemale }}</td>
          <td>{{ censusData.dcPhswTotal }}</td>
        </tr>
        <tr>
          <th scope="row">Philadelphia Industrial Correctional Center</th>
          <td>{{ censusData.piccMale }}</td>
          <td>{{ censusData.piccFemale }}</td>
          <td>{{ censusData.piccMaleJuv }}</td>
          <td>{{ censusData.piccFemaleJuv }}</td>
          <td>{{ censusData.piccNifWorkerMale }}</td>
          <td>{{ censusData.piccNifWorkerFemale }}</td>
          <td>{{ censusData.piccNifFurMale }}</td>
          <td>{{ censusData.piccNifFurFemale }}</td>
          <td>{{ censusData.piccNifOwMale }}</td>
          <td>{{ censusData.piccNifOwFemale }}</td>
          <td>{{ censusData.piccNifEtMale }}</td>
          <td>{{ censusData.piccNifEtFemale }}</td>
          <td>{{ censusData.piccTotal }}</td>
        </tr>
        <tr>
          <th scope="row">Riverside Correctional Facility</th>
          <td>{{ censusData.rcfMale }}</td>
          <td>{{ censusData.rcfFemale }}</td>
          <td>{{ censusData.rcfMaleJuv }}</td>
          <td>{{ censusData.rcfFemaleJuv }}</td>
          <td>{{ censusData.rcfNifWorkerMale }}</td>
          <td>{{ censusData.rcfNifWorkerFemale }}</td>
          <td>{{ censusData.rcfNifFurMale }}</td>
          <td>{{ censusData.rcfNifFurFemale }}</td>
          <td>{{ censusData.rcfNifOwMale }}</td>
          <td>{{ censusData.rcfNifOwFemale }}</td>
          <td>{{ censusData.rcfNifEtMale }}</td>
          <td>{{ censusData.rcfNifEtFemale }}</td>
          <td>{{ censusData.rcfTotal }}</td>
        </tr>
        <tr>
          <th scope="row">Weekenders</th>
          <td>{{ censusData.weekendersMale }}</td>
          <td>{{ censusData.weekendersFemale }}</td>
          <td>{{ censusData.weekendersMaleJuv }}</td>
          <td>{{ censusData.weekendersFemaleJuv }}</td>
          <td>{{ censusData.weekendersNifWorkerMale }}</td>
          <td>{{ censusData.weekendersNifWorkerFemale }}</td>
          <td>{{ censusData.weekendersNifFurMale }}</td>
          <td>{{ censusData.weekendersNifFurFemale }}</td>
          <td>{{ censusData.weekendersNifOwMale }}</td>
          <td>{{ censusData.weekendersNifOwFemale }}</td>
          <td>{{ censusData.weekendersNifEtMale }}</td>
          <td>{{ censusData.weekendersNifEtFemale }}</td>
          <td>{{ censusData.weekendersTotal }}</td>
        </tr>
        <tr>
          <th scope="row">PDP "In Facility" Headcount Total</th>
          <td><strong>{{ censusData.pdpInFacilityCountMale }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountFemale }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountMaleJuv }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountFemaleJuv }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountNifWorkerMale }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountNifWorkerFemale }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountNifFurMale }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountNifFurFemale }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountNifOwMale }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountNifOwFemale }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountNifEtMale }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountNifEtFemale }}</strong></td>
          <td><strong>{{ censusData.pdpInFacilityCountTotal }}</strong></td>
        </tr>
      </tbody>
    </table>

    <table>
      <thead>
        <tr>
          <th></th>
          <th>Male</th>
          <th>Female</th>
          <th>Total</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th scope="row" class="half-width">Adult + Juvenile Total "In Facility" Count</th>
          <td>{{ censusData.pdpInFacilityCountMaleAdultsJuv }}</td>
          <td>{{ censusData.pdpInFacilityCountFemaleAdultsJuv }}</td>
          <td>{{ censusData.pdpInFacilityCountTotalAdultsJuv }}</td>
        </tr>
        <tr>
          <th scope="row" class="half-width">Not in Facility (NIF) Total</th>
          <td>{{ censusData.nifMale }}</td>
           <td>{{ censusData.nifFemale }}</td>
          <td>{{ censusData.nifTotal }}</td>
        </tr>
         <tr>
          <th scope="row" class="half-width">PDP "In Facility" Headcount + NIF Total</th>
          <td>{{ censusData.pdpHeadcountNifMale }}</td>
           <td>{{ censusData.pdpHeadcountNifFemale }}</td>
          <td>{{ censusData.pdpHeadcountNifTotal }}</td>
        </tr>
         <tr>
          <th scope="row" class="half-width">Other Jursidictions (OJ) Total</th>
          <td>{{ censusData.ojMale }}</td>
           <td>{{ censusData.ojFemale }}</td>
          <td>{{ censusData.ojTotal }}</td>
        </tr>
         <tr>
          <th scope="row" class="half-width">PDP Headcount + NIF + OJ (Census) Total</th>
          <td>{{ censusData.pdpHeadcountNifOjMale }}</td>
           <td>{{ censusData.pdpHeadcountNifOjFemale }}</td>
          <td>{{ censusData.pdpHeadcountNifOjTotal }}</td>
        </tr>
         <tr>
          <th scope="row" class="half-width">State Department of Corrections (DOC)</th>
          <td>{{ censusData.oocStateDocMale }}</td>
           <td>{{ censusData.oocStateDocFemale }}</td>
          <td>{{ censusData.oocStateDocTotal }}</td>
        </tr>
         <tr>
          <th scope="row" class="half-width">Juveniles</th>
          <td>{{ censusData.oocJuvMale }}</td>
           <td>{{ censusData.oocJuvFemale }}</td>
          <td>{{ censusData.oocJuvTotal }}</td>
        </tr>
         <tr>
          <th scope="row" class="half-width">Delaware County</th>
          <td>{{ censusData.oocDelMale }}</td>
           <td>{{ censusData.oocDelFemale }}</td>
          <td>{{ censusData.oocDelTotal }}</td>
        </tr>
         <tr>
          <th scope="row" class="half-width">Lehigh County</th>
          <td>{{ censusData.oocLehighMale }}</td>
           <td>{{ censusData.oocLehighFemale }}</td>
          <td>{{ censusData.oocLehighTotal }}</td>
        </tr>
         <tr>
          <th scope="row" class="half-width">CEC</th>
          <td>{{ censusData.oocCecMale }}</td>
           <td>{{ censusData.oocCecFemale }}</td>
          <td>{{ censusData.oocCecTotal }}</td>
        </tr>
         <tr>
          <th scope="row" class="half-width">ROTH</th>
          <td>{{ censusData.oocRothMale }}</td>
           <td>{{ censusData.oocRothFemale }}</td>
          <td>{{ censusData.oocRothTotal }}</td>
        </tr>
         <tr>
          <th scope="row" class="half-width">Total</th>
          <td><strong>{{ censusData.censusMale }}</strong></td>
          <td><strong>{{ censusData.censusFemale }}</strong></td>
          <td><strong>{{ censusData.censusTotal }}</strong></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
// import Vue from "vue";

const endpoint =
  "https://api.phila.gov/inmate-locator/census?gatekeeperKey=c1cfa6750fa0517fbdefeb90a1464004";

export default {
  name: "DailyCensus",
  data: function() {
    return {
      censusData: [],
      loading: false,
      failure: false,
      empty: false
    };
  },

  mounted() {
    this.fetchData();
  },

  watch: {},

  methods: {
    fetchData: function() {
      this.loading = true;
      axios
        .get(endpoint)
        .then(response => {
          this.censusData = response.data;
          this.failure = false;
          this.loading = false;
        })
        .catch(e => {
          console.log(e);
          this.loading = false;
          this.failure = true;
        });
    }
  }
};
</script>

<style scoped>
.half-width {
  width: 50%;
}
</style>