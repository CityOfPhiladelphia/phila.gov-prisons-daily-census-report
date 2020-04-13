<template>
  <div>
    {{ censusData }}
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
          <th scope="row">rcf asdcu</th>
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
          <th scope="row">cfcf</th>
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
          <th scope="row">dc</th>
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
          <th scope="row">dcPhsw</th>
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
          <th scope="row">picc</th>
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
          <th scope="row">rcf</th>
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
          <th scope="row">weekenders</th>
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
          <th scope="row">total</th>
          <td>{{ censusData.pdpInFacilityCountMale }}</td>
          <td>{{ censusData.pdpInFacilityCountFemale }}</td>
          <td>{{ censusData.pdpInFacilityCountMaleJuv }}</td>
          <td>{{ censusData.pdpInFacilityCountFemaleJuv }}</td>
          <td>{{ censusData.pdpInFacilityCountNifWorkerMale }}</td>
          <td>{{ censusData.pdpInFacilityCountNifWorkerFemale }}</td>
          <td>{{ censusData.pdpInFacilityCountNifFurMale }}</td>
          <td>{{ censusData.pdpInFacilityCountNifFurFemale }}</td>
          <td>{{ censusData.pdpInFacilityCountNifOwMale }}</td>
          <td>{{ censusData.pdpInFacilityCountNifOwFemale }}</td>
          <td>{{ censusData.pdpInFacilityCountNifEtMale }}</td>
          <td>{{ censusData.pdpInFacilityCountNifEtFemale }}</td>
          <td>{{ censusData.pdpInFacilityCountTotal }}</td>
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
          <th scope="row">pdpInFacilityCount</th>
          <td>{{ censusData.pdpInFacilityCountMaleAdultsJuv }}</td>
          <td>{{ censusData.pdpInFacilityCountFemaleAdultsJuv }}</td>
          <td>{{ censusData.pdpInFacilityCountTotalAdultsJuv }}</td>
        </tr>
        <tr>
          <th scope="row">nif</th>
          <td>{{ censusData.nifMale }}</td>
           <td>{{ censusData.nifFemale }}</td>
          <td>{{ censusData.nifTotal }}</td>
        </tr>
         <tr>
          <th scope="row">pdpHeadcountNif</th>
          <td>{{ censusData.pdpHeadcountNifMale }}</td>
           <td>{{ censusData.pdpHeadcountNifFemale }}</td>
          <td>{{ censusData.pdpHeadcountNifTotal }}</td>
        </tr>
         <tr>
          <th scope="row">oj</th>
          <td>{{ censusData.ojMale }}</td>
           <td>{{ censusData.ojFemale }}</td>
          <td>{{ censusData.ojTotal }}</td>
        </tr>
         <tr>
          <th scope="row">pdpHeadcountNifOj</th>
          <td>{{ censusData.pdpHeadcountNifOjMale }}</td>
           <td>{{ censusData.pdpHeadcountNifOjFemale }}</td>
          <td>{{ censusData.pdpHeadcountNifOjTotal }}</td>
        </tr>
         <tr>
          <th scope="row">oocStateDoc</th>
          <td>{{ censusData.oocStateDocMale }}</td>
           <td>{{ censusData.oocStateDocFemale }}</td>
          <td>{{ censusData.oocStateDocTotal }}</td>
        </tr>
         <tr>
          <th scope="row">oocJuv</th>
          <td>{{ censusData.oocJuvMale }}</td>
           <td>{{ censusData.oocJuvFemale }}</td>
          <td>{{ censusData.oocJuvTotal }}</td>
        </tr>
         <tr>
          <th scope="row">oocDel</th>
          <td>{{ censusData.oocDelMale }}</td>
           <td>{{ censusData.oocDelFemale }}</td>
          <td>{{ censusData.oocDelTotal }}</td>
        </tr>
         <tr>
          <th scope="row">oocLehigh</th>
          <td>{{ censusData.oocLehighMale }}</td>
           <td>{{ censusData.oocLehighFemale }}</td>
          <td>{{ censusData.oocLehighTotal }}</td>
        </tr>
         <tr>
          <th scope="row">oocCec</th>
          <td>{{ censusData.oocCecMale }}</td>
           <td>{{ censusData.oocCecFemale }}</td>
          <td>{{ censusData.oocCecTotal }}</td>
        </tr>
         <tr>
          <th scope="row">oocRoth</th>
          <td>{{ censusData.oocRothMale }}</td>
           <td>{{ censusData.oocRothFemale }}</td>
          <td>{{ censusData.oocRothTotal }}</td>
        </tr>
         <tr>
          <th scope="row">census</th>
          <td>{{ censusData.censusMale }}</td>
           <td>{{ censusData.censusFemale }}</td>
          <td>{{ censusData.censusTotal }}</td>
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
</style>