<template>
  <div>
    <p>Daily census report for {{ censusData.date | toReadableDate }}</p>
    <div v-show="loading" class="mtm center">
      <i class="fas fa-spinner fa-spin fa-3x" />
    </div>
    <div v-show="!loading && empty" class="h3 mtm center">Sorry, there are no results.</div>
    <div v-show="failure" class="h3 mtm center">Sorry, there was a problem. Please try again.</div>
    <h1>In Facility</h1>
    <table v-show="!empty && !loading && !failure">
      <thead>
        <tr>
          <th scope="col">Facility</th>
          <th scope="col">Adult male</th>
          <th scope="col">Adult female</th>
          <th scope="col">Juvenile male</th>
          <th scope="col">Juvenile female</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Riverside Correctional Facility Alternative and Special Detention Central Unit</td>
          <td>{{ censusData.asdcuMale | rmZero }}</td>
          <td>{{ censusData.asdcuFemale | rmZero }}</td>
          <td>{{ censusData.asdcuMaleJuv | rmZero }}</td>
          <td>{{ censusData.asdcuFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Curran-Fromhold Correctional Facility</td>
          <td>{{ censusData.cfcfMale | rmZero }}</td>
          <td>{{ censusData.cfcfFemale | rmZero }}</td>
          <td>{{ censusData.cfcfMaleJuv | rmZero }}</td>
          <td>{{ censusData.cfcfFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Detention Center</td>
          <td>{{ censusData.dcMale | rmZero }}</td>
          <td>{{ censusData.dcFemale | rmZero }}</td>
          <td>{{ censusData.dcMaleJuv | rmZero }}</td>
          <td>{{ censusData.dcFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Detention Center Public Health Services Wing</td>
          <td>{{ censusData.dcPhswMale | rmZero }}</td>
          <td>{{ censusData.dcPhswFemale | rmZero }}</td>
          <td>{{ censusData.dcPhswMaleJuv | rmZero }}</td>
          <td>{{ censusData.dcPhswFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Philadelphia Industrial Correctional Center</td>
          <td>{{ censusData.piccMale | rmZero }}</td>
          <td>{{ censusData.piccFemale | rmZero }}</td>
          <td>{{ censusData.piccMaleJuv | rmZero }}</td>
          <td>{{ censusData.piccFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Riverside Correctional Facility</td>
          <td>{{ censusData.rcfMale | rmZero }}</td>
          <td>{{ censusData.rcfFemale | rmZero }}</td>
          <td>{{ censusData.rcfMaleJuv | rmZero }}</td>
          <td>{{ censusData.rcfFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Weekenders</td>
          <td>{{ censusData.weekendersMale | rmZero }}</td>
          <td>{{ censusData.weekendersFemale | rmZero }}</td>
          <td>{{ censusData.weekendersMaleJuv | rmZero }}</td>
          <td>{{ censusData.weekendersFemaleJuv | rmZero }}</td>
        </tr>
        <tr class="blue-row">
          <td>PDP "In Facility" Headcount Total</td>
          <td>{{ censusData.pdpInFacilityCountMale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountFemale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountMaleJuv | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountFemaleJuv | rmZero }}</td>
        </tr>
      </tbody>
    </table>

    <h1>Not in facility</h1>
    <table v-show="!empty && !loading && !failure">
      <thead>
        <tr>
          <th scope="col">Facility</th>
          <th scope="col">Male workers</th>
          <th scope="col">Female workers</th>
          <th scope="col">Male furlough</th>
          <th scope="col">Female furlough</th>
          <th scope="col">Male open ward</th>
          <th scope="col">Female open ward</th>
          <th scope="col">Male emergency trips</th>
          <th scope="col">Female emergency trips</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Riverside Correctional Facility Alternative and Special Detention Central Unit</td>
          <td>{{ censusData.asdcuNifWorkerMale | rmZero }}</td>
          <td>{{ censusData.asdcuNifWorkerFemale | rmZero }}</td>
          <td>{{ censusData.asdcuNifFurMale | rmZero }}</td>
          <td>{{ censusData.asdcuNifFurFemale | rmZero }}</td>
          <td>{{ censusData.asdcuNifOwMale | rmZero }}</td>
          <td>{{ censusData.asdcuNifOwFemale | rmZero }}</td>
          <td>{{ censusData.asdcuNifEtMale | rmZero }}</td>
          <td>{{ censusData.asdcuNifEtFemale | rmZero }}</td>
        </tr>
        <tr>
          <td>Curran-Fromhold Correctional Facility</td>
          <td>{{ censusData.cfcfNifWorkerMale | rmZero }}</td>
          <td>{{ censusData.cfcfNifWorkerFemale | rmZero }}</td>
          <td>{{ censusData.cfcfNifFurMale | rmZero }}</td>
          <td>{{ censusData.cfcfNifFurFemale | rmZero }}</td>
          <td>{{ censusData.cfcfNifOwMale | rmZero }}</td>
          <td>{{ censusData.cfcfNifOwFemale | rmZero }}</td>
          <td>{{ censusData.cfcfNifEtMale | rmZero }}</td>
          <td>{{ censusData.cfcfNifEtFemale | rmZero }}</td>
        </tr>
        <tr>
          <td>Detention Center</td>
          <td>{{ censusData.dcNifWorkerMale | rmZero }}</td>
          <td>{{ censusData.dcNifWorkerFemale | rmZero }}</td>
          <td>{{ censusData.dcNifFurMale | rmZero }}</td>
          <td>{{ censusData.dcNifFurFemale | rmZero }}</td>
          <td>{{ censusData.dcNifOwMale | rmZero }}</td>
          <td>{{ censusData.dcNifOwFemale | rmZero }}</td>
          <td>{{ censusData.dcNifEtMale | rmZero }}</td>
          <td>{{ censusData.dcNifEtFemale | rmZero }}</td>
        </tr>
        <tr>
          <td>Detention Center Public Health Services Wing</td>
          <td>{{ censusData.dcPhswNifWorkerMale | rmZero }}</td>
          <td>{{ censusData.dcPhswNifWorkerFemale | rmZero }}</td>
          <td>{{ censusData.dcPhswNifFurMale | rmZero }}</td>
          <td>{{ censusData.dcPhswNifFurFemale | rmZero }}</td>
          <td>{{ censusData.dcPhswNifOwMale | rmZero }}</td>
          <td>{{ censusData.dcPhswNifOwFemale | rmZero }}</td>
          <td>{{ censusData.dcPhswNifEtMale | rmZero }}</td>
          <td>{{ censusData.dcPhswNifEtFemale | rmZero }}</td>
        </tr>
        <tr>
          <td>Philadelphia Industrial Correctional Center</td>
          <td>{{ censusData.piccNifWorkerMale | rmZero }}</td>
          <td>{{ censusData.piccNifWorkerFemale | rmZero }}</td>
          <td>{{ censusData.piccNifFurMale | rmZero }}</td>
          <td>{{ censusData.piccNifFurFemale | rmZero }}</td>
          <td>{{ censusData.piccNifOwMale | rmZero }}</td>
          <td>{{ censusData.piccNifOwFemale | rmZero }}</td>
          <td>{{ censusData.piccNifEtMale | rmZero }}</td>
          <td>{{ censusData.piccNifEtFemale | rmZero }}</td>
        </tr>
        <tr>
          <td>Riverside Correctional Facility</td>
          <td>{{ censusData.rcfNifWorkerMale | rmZero }}</td>
          <td>{{ censusData.rcfNifWorkerFemale | rmZero }}</td>
          <td>{{ censusData.rcfNifFurMale | rmZero }}</td>
          <td>{{ censusData.rcfNifFurFemale | rmZero }}</td>
          <td>{{ censusData.rcfNifOwMale | rmZero }}</td>
          <td>{{ censusData.rcfNifOwFemale | rmZero }}</td>
          <td>{{ censusData.rcfNifEtMale | rmZero }}</td>
          <td>{{ censusData.rcfNifEtFemale | rmZero }}</td>
        </tr>
        <tr>
          <td>Weekenders</td>
          <td>{{ censusData.weekendersNifWorkerMale | rmZero }}</td>
          <td>{{ censusData.weekendersNifWorkerFemale | rmZero }}</td>
          <td>{{ censusData.weekendersNifFurMale | rmZero }}</td>
          <td>{{ censusData.weekendersNifFurFemale | rmZero }}</td>
          <td>{{ censusData.weekendersNifOwMale | rmZero }}</td>
          <td>{{ censusData.weekendersNifOwFemale | rmZero }}</td>
          <td>{{ censusData.weekendersNifEtMale | rmZero }}</td>
          <td>{{ censusData.weekendersNifEtFemale | rmZero }}</td>
        </tr>
        <tr class="blue-row">
          <td>PDP "Not In Facility" Headcount Total</td>
          <td>{{ censusData.pdpInFacilityCountNifWorkerMale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountNifWorkerFemale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountNifFurMale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountNifFurFemale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountNifOwMale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountNifOwFemale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountNifEtMale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountNifEtFemale | rmZero }}</td>
        </tr>
      </tbody>
    </table>
    <h1>In facility and not in facility totals</h1>
    <table v-show="!empty && !loading && !failure">
      <thead>
        <tr>
          <th scope="col">Facility</th>
          <th scope="col">Male</th>
          <th scope="col">Female</th>
          <th scope="col">Total</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Riverside Correctional Facility Alternative and Special Detention Central Unit</td>
          <td>{{ censusData.asdcuMale + censusData.asdcuMaleJuv + censusData.asdcuNifFurMale + censusData.asdcuNifOwMale + censusData.asdcuNifEtMale | rmZero }}</td>
          <td>{{ censusData.asdcuFemale + censusData.asdcuFemaleJuv + censusData.asdcuNifFurFemale + censusData.asdcuNifOwFemale + censusData.asdcuNifEtFemale | rmZero }}</td>
          <td>{{ censusData.asdcuTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Curran-Fromhold Correctional Facility</td>
          <td>{{ censusData.cfcfMale + censusData.cfcfMaleJuv + censusData.cfcfNifFurMale + censusData.cfcfNifOwMale + censusData.cfcfNifEtMale | rmZero }}</td>
          <td>{{ censusData.cfcfFemale + censusData.cfcfFemaleJuv + censusData.cfcfNifFurFemale + censusData.cfcfNifOwFemale + censusData.cfcfNifEtFemale | rmZero }}</td>
          <td>{{ censusData.cfcfTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Detention Center</td>
          <td>{{ censusData.dcMale + censusData.dcMaleJuv + censusData.dcNifFurMale + censusData.dcNifOwMale + censusData.dcNifEtMale | rmZero }}</td>
          <td>{{ censusData.dcFemale + censusData.dcFemaleJuv + censusData.dcNifFurFemale + censusData.dcNifOwFemale + censusData.dcNifEtFemale | rmZero }}</td>
          <td>{{ censusData.dcTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Detention Center Public Health Services Wing</td>
          <td>{{ censusData.dcPhswMale + censusData.dcPhswMaleJuv + censusData.dcPhswNifFurMale + censusData.dcPhswNifOwMale + censusData.dcPhswNifEtMale | rmZero }}</td>
          <td>{{ censusData.dcPhswFemale + censusData.dcPhswFemaleJuv + censusData.dcPhswNifFurFemale + censusData.dcPhswNifOwFemale + censusData.dcPhswNifEtFemale | rmZero }}</td>
          <td>{{ censusData.dcPhswTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Philadelphia Industrial Correctional Center</td>
          <td>{{ censusData.piccMale + censusData.piccMaleJuv + censusData.piccNifFurMale + censusData.piccNifOwMale + censusData.piccNifEtMale | rmZero }}</td>
          <td>{{ censusData.piccFemale + censusData.piccFemaleJuv + censusData.piccNifFurFemale + censusData.piccNifOwFemale + censusData.piccNifEtFemale | rmZero }}</td>
          <td>{{ censusData.piccTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Riverside Correctional Facility</td>

          <td>{{ censusData.rcfMale + censusData.rcfMaleJuv + censusData.rcfNifFurMale + censusData.rcfNifOwMale + censusData.rcfNifEtMale | rmZero }}</td>
          <td>{{ censusData.rcfFemale + censusData.rcfFemaleJuv + censusData.rcfNifFurFemale + censusData.rcfNifOwFemale + censusData.rcfNifEtFemale | rmZero }}</td>
          <td>{{ censusData.rcfTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Weekenders</td>
          <td>{{ censusData.weekendersMale + censusData.weekendersMaleJuv + censusData.weekendersNifFurMale + censusData.weekendersNifOwMale + censusData.weekendersNifEtMale | rmZero }}</td>
          <td>{{ censusData.weekendersFemale + censusData.weekendersFemaleJuv + censusData.weekendersNifFurFemale + censusData.weekendersNifOwFemale + censusData.weekendersNifEtFemale | rmZero }}</td>
          <td>{{ censusData.weekendersTotal | rmZero }}</td>
        </tr>
        <tr class="blue-row">
          <td>PDP "In Facility" Headcount + NIF Total</td>
          <td>{{ censusData.pdpHeadcountNifMale | rmZero }}</td>
          <td>{{ censusData.pdpHeadcountNifFemale | rmZero }}</td>
          <td>{{ censusData.pdpHeadcountNifTotal | rmZero }}</td>
        </tr>
      </tbody>
    </table>
    <h1>Other totals?</h1>
    <table>
      <thead>
        <tr>
          <th>Location</th>
          <th>Male</th>
          <th>Female</th>
          <th>Total</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="half-width">Adult + Juvenile Total "In Facility" Count</td>
          <td>{{ censusData.pdpInFacilityCountMaleAdultsJuv | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountFemaleAdultsJuv | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountTotalAdultsJuv | rmZero }}</td>
        </tr>
        <tr>
          <td class="half-width">Not in Facility (NIF) Total</td>
          <td>{{ censusData.nifMale | rmZero }}</td>
          <td>{{ censusData.nifFemale | rmZero }}</td>
          <td>{{ censusData.nifTotal | rmZero }}</td>
        </tr>
        <tr class="light-blue-row">
          <td class="half-width">PDP "In Facility" Headcount + NIF Total</td>
          <td>{{ censusData.pdpHeadcountNifMale | rmZero }}</td>
          <td>{{ censusData.pdpHeadcountNifFemale | rmZero }}</td>
          <td>{{ censusData.pdpHeadcountNifTotal | rmZero }}</td>
        </tr>
      </tbody>
    </table>
    <table>
      <tbody>
        <tr>
          <td class="half-width">Other Jursidictions (OJ) Total</td>
          <td>{{ censusData.ojMale | rmZero }}</td>
          <td>{{ censusData.ojFemale | rmZero }}</td>
          <td>{{ censusData.ojTotal | rmZero }}</td>
        </tr>
        <tr class="light-blue-row">
          <td class="half-width">PDP Headcount + NIF + OJ (Census) Total</td>
          <td>{{ censusData.pdpHeadcountNifOjMale | rmZero }}</td>
          <td>{{ censusData.pdpHeadcountNifOjFemale | rmZero }}</td>
          <td>{{ censusData.pdpHeadcountNifOjTotal | rmZero }}</td>
        </tr>
      </tbody>
    </table>

    <table>
      <tbody>
        <tr>
          <td class="half-width">State Department of Corrections (DOC)</td>
          <td>{{ censusData.oocStateDocMale | rmZero }}</td>
          <td>{{ censusData.oocStateDocFemale | rmZero }}</td>
          <td>{{ censusData.oocStateDocTotal | rmZero }}</td>
        </tr>
        <tr>
          <td class="half-width">Juveniles</td>
          <td>{{ censusData.oocJuvMale | rmZero }}</td>
          <td>{{ censusData.oocJuvFemale | rmZero }}</td>
          <td>{{ censusData.oocJuvTotal | rmZero }}</td>
        </tr>
        <tr>
          <td class="half-width">Delaware County</td>
          <td>{{ censusData.oocDelMale | rmZero }}</td>
          <td>{{ censusData.oocDelFemale | rmZero }}</td>
          <td>{{ censusData.oocDelTotal | rmZero }}</td>
        </tr>
        <tr>
          <td class="half-width">Lehigh County</td>
          <td>{{ censusData.oocLehighMale | rmZero }}</td>
          <td>{{ censusData.oocLehighFemale | rmZero }}</td>
          <td>{{ censusData.oocLehighTotal | rmZero }}</td>
        </tr>
        <tr>
          <td class="half-width">CEC</td>
          <td>{{ censusData.oocCecMale | rmZero }}</td>
          <td>{{ censusData.oocCecFemale | rmZero }}</td>
          <td>{{ censusData.oocCecTotal | rmZero }}</td>
        </tr>
        <tr>
          <td class="half-width">ROTH</td>
          <td>{{ censusData.oocRothMale | rmZero }}</td>
          <td>{{ censusData.oocRothFemale | rmZero }}</td>
          <td>{{ censusData.oocRothTotal | rmZero }}</td>
        </tr>
        <tr class="blue-row">
          <td class="half-width">Total</td>
          <td>{{ censusData.censusMale | rmZero }}</td>
          <td>{{ censusData.censusFemale | rmZero }}</td>
          <td>{{ censusData.censusTotal | rmZero }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
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

  filters: {
    rmZero(val) {
      if (val === 0) {
        return "";
      } else {
        return val;
      }
    },

    toReadableDate(val) {
      return moment(val).format('MMMM DD, YYYY')
    }
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

.blue-row td {
  background-color: #0f4d90;
  color: white;
}

.light-blue-row td {
  background-color: #2176d2;
  color: white;
}
</style>