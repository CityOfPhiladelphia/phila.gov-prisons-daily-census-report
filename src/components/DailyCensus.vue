<template>
  <div>
    <div v-show="loading" class="mtm center">
      <i class="fas fa-spinner fa-spin fa-3x" />
    </div>
    <div v-show="!loading && empty" class="h3 mtm center">Sorry, there are no results.</div>
    <div v-show="failure" class="h3 mtm center">Sorry, there was a problem. Please try again.</div>
    <div v-show="!empty && !loading && !failure">
      <div class="mbxl">
    <p>Census for: {{ censusData.date | toReadableDate }}</p>
    <p>The Philadelphia Department of Prisons (PDP) posts a census of its inmates every day. The census includes a headcount of inmates in each facility. In some cases, a facility is responsible for an inmate who is temporarily outside that facility.
    </p>

     <p> <a href="#if">In Facility </a> - The total number of inmates currently in custody at a PDP facility. These inmates are physically inside each facility. <br> </p>
     <p><a href="#nif">Temporarily not in facility </a> - The total number of inmates who are usually in a PDP facility, but are temporarily in another location. This includes four categories: workers, furlough, open ward, and emergency trips. 
<ul>
<li>Workers are outside the facility itself, but working on campus. </li>
<li>Furloughs are authorized absences from the facility. </li>
<li>Open ward inmates have been admitted to a hospital. </li>
<li>Emergency trips include any inmates who have been taken to the hospital, but not yet admitted. </li>
</ul>
</p>
     <p><a href="#ifnif">PDP facility totals</a>  - The total number of inmates that each facility is responsible for. This includes both inmates in the facility and inmates who are temporarily not in the facility. <br> </p>
     <p><a href="#other">PDP inmates held in other jurisdictions </a> - The total number of inmates that PDP is responsible for, but are in custody outside of the PDP system. <br> </p>
     <p><a href="#total"> PDP total population </a> - The grand total of inmates that PDP is responsible for. This includes inmates who are in PDP facilities, temporarily out of PDP facilities, and being held in other jurisdictions.  </p>
    </div>
    <h3><div id="if">In Facility</div></h3>
    <table >
      <thead>
        <tr>
          <th scope="col">Facility</th>
          <th scope="col">Adult males</th>
          <th scope="col">Adult females</th>
          <th scope="col">Juvenile males</th>
          <th scope="col">Juvenile females</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Riverside Correctional Facility Alternative and Special Detention Central Unit (RCF ASDCU)</td>
          <td>{{ censusData.asdcuMale | rmZero }}</td>
          <td>{{ censusData.asdcuFemale | rmZero }}</td>
          <td>{{ censusData.asdcuMaleJuv | rmZero }}</td>
          <td>{{ censusData.asdcuFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Curran-Fromhold Correctional Facility (CFCF)</td>
          <td>{{ censusData.cfcfMale | rmZero }}</td>
          <td>{{ censusData.cfcfFemale | rmZero }}</td>
          <td>{{ censusData.cfcfMaleJuv | rmZero }}</td>
          <td>{{ censusData.cfcfFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Detention Center (DC)</td>
          <td>{{ censusData.dcMale | rmZero }}</td>
          <td>{{ censusData.dcFemale | rmZero }}</td>
          <td>{{ censusData.dcMaleJuv | rmZero }}</td>
          <td>{{ censusData.dcFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Detention Center Public Health Services Wing (DC PHSW)</td>
          <td>{{ censusData.dcPhswMale | rmZero }}</td>
          <td>{{ censusData.dcPhswFemale | rmZero }}</td>
          <td>{{ censusData.dcPhswMaleJuv | rmZero }}</td>
          <td>{{ censusData.dcPhswFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Philadelphia Industrial Correctional Center (PICC)</td>
          <td>{{ censusData.piccMale | rmZero }}</td>
          <td>{{ censusData.piccFemale | rmZero }}</td>
          <td>{{ censusData.piccMaleJuv | rmZero }}</td>
          <td>{{ censusData.piccFemaleJuv | rmZero }}</td>
        </tr>
        <tr>
          <td>Riverside Correctional Facility (RCF)</td>
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
          <td>In facility headcount total</td>
          <td>{{ censusData.pdpInFacilityCountMale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountFemale | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountMaleJuv | rmZero }}</td>
          <td>{{ censusData.pdpInFacilityCountFemaleJuv | rmZero }}</td>
        </tr>
      </tbody>
    </table>

    <h3><div id="nif">Temporarily not in facility</div></h3>
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
          <td>Riverside Correctional Facility Alternative and Special Detention Central Unit (RCF ASDCU)</td>
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
          <td>Curran-Fromhold Correctional Facility (CFCF)</td>
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
          <td>Detention Center (DC)</td>
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
          <td>Detention Center Public Health Services Wing (DC PHSW)</td>
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
          <td>Philadelphia Industrial Correctional Center (PICC)</td>
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
          <td>Riverside Correctional Facility (RCF)</td>
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
          <td>Temporarily not in facility total</td>
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
    <h3><div id="ifnif">PDP facility totals (both in facility and temporarily not in facility totals)</div></h3>
    <table v-show="!empty && !loading && !failure">
      <thead>
        <tr>
          <th scope="col">Facility</th>
          <th scope="col">Males</th>
          <th scope="col">Females</th>
          <th scope="col">Total</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Riverside Correctional Facility Alternative and Special Detention Central Unit (RCF ASDCU)</td>
          <td>{{ censusData.asdcuMale + censusData.asdcuMaleJuv + censusData.asdcuNifFurMale + censusData.asdcuNifOwMale + censusData.asdcuNifEtMale | rmZero }}</td>
          <td>{{ censusData.asdcuFemale + censusData.asdcuFemaleJuv + censusData.asdcuNifFurFemale + censusData.asdcuNifOwFemale + censusData.asdcuNifEtFemale | rmZero }}</td>
          <td>{{ censusData.asdcuTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Curran-Fromhold Correctional Facility (CFCF)</td>
          <td>{{ censusData.cfcfMale + censusData.cfcfMaleJuv + censusData.cfcfNifFurMale + censusData.cfcfNifOwMale + censusData.cfcfNifEtMale | rmZero }}</td>
          <td>{{ censusData.cfcfFemale + censusData.cfcfFemaleJuv + censusData.cfcfNifFurFemale + censusData.cfcfNifOwFemale + censusData.cfcfNifEtFemale | rmZero }}</td>
          <td>{{ censusData.cfcfTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Detention Center (DC)</td>
          <td>{{ censusData.dcMale + censusData.dcMaleJuv + censusData.dcNifFurMale + censusData.dcNifOwMale + censusData.dcNifEtMale | rmZero }}</td>
          <td>{{ censusData.dcFemale + censusData.dcFemaleJuv + censusData.dcNifFurFemale + censusData.dcNifOwFemale + censusData.dcNifEtFemale | rmZero }}</td>
          <td>{{ censusData.dcTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Detention Center Public Health Services Wing (DC PHSW)</td>
          <td>{{ censusData.dcPhswMale + censusData.dcPhswMaleJuv + censusData.dcPhswNifFurMale + censusData.dcPhswNifOwMale + censusData.dcPhswNifEtMale | rmZero }}</td>
          <td>{{ censusData.dcPhswFemale + censusData.dcPhswFemaleJuv + censusData.dcPhswNifFurFemale + censusData.dcPhswNifOwFemale + censusData.dcPhswNifEtFemale | rmZero }}</td>
          <td>{{ censusData.dcPhswTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Philadelphia Industrial Correctional Center (PICC)</td>
          <td>{{ censusData.piccMale + censusData.piccMaleJuv + censusData.piccNifFurMale + censusData.piccNifOwMale + censusData.piccNifEtMale | rmZero }}</td>
          <td>{{ censusData.piccFemale + censusData.piccFemaleJuv + censusData.piccNifFurFemale + censusData.piccNifOwFemale + censusData.piccNifEtFemale | rmZero }}</td>
          <td>{{ censusData.piccTotal | rmZero }}</td>
        </tr>
        <tr>
          <td>Riverside Correctional Facility (RCF)</td>

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
          <td>In facility headcount and temporarily not in facility total</td>
          <td>{{ censusData.pdpHeadcountNifMale | rmZero }}</td>
          <td>{{ censusData.pdpHeadcountNifFemale | rmZero }}</td>
          <td>{{ censusData.pdpHeadcountNifTotal | rmZero }}</td>
        </tr>
      </tbody>
    </table>
    <h3><div id="other">PDP inmates held in other jurisdictions</div></h3>
    <table>
      <thead>
        <tr>
          <th scope="col">Jurisdiction</th>
          <th scope="col">Males</th>
          <th scope="col">Females</th>
          <th scope="col">Total</th>
        </tr>
      </thead>
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
        <tr >
          <td class="half-width">Other jurisdictions</td>
          <td>{{ censusData.ojMale | rmZero }}</td>
          <td>{{ censusData.ojFemale | rmZero }}</td>
          <td>{{ censusData.ojTotal | rmZero }}</td>
        </tr>
        <tr class="blue-row">
          <td class="half-width">Totals</td>
          <td>{{ censusData.ojMale +  censusData.oocRothMale + censusData.oocCecMale + censusData.oocLehighMale + censusData.oocJuvMale + censusData.oocDelMale +  censusData.oocStateDocMale | rmZero }}</td>
          <td>{{ censusData.ojFemale +  censusData.oocRothFemale + censusData.oocCecFemale + censusData.oocLehighFemale + censusData.oocJuvFemale + censusData.oocDelFemale +  censusData.oocStateDocFemale | rmZero }}</td>
          <td>{{ censusData.ojTotal +  censusData.oocRothTotal + censusData.oocCecTotal + censusData.oocLehighTotal + censusData.oocJuvTotal + censusData.oocDelTotal +  censusData.oocStateDocTotal | rmZero }}</td>
        </tr>
      </tbody>
    </table>
    <h3><div id="total">PDP total population</div></h3>
    
    <table>
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col">Males</th>
          <th scope="col">Females</th>
          <th scope="col">Total</th>
        </tr>
      </thead>
      <tbody>
       <tr >
          <td>PDP in facility headcount and temporarily not in facility total</td>
          <td>{{ censusData.pdpHeadcountNifMale | rmZero }}</td>
          <td>{{ censusData.pdpHeadcountNifFemale | rmZero }}</td>
          <td>{{ censusData.pdpHeadcountNifTotal | rmZero }}</td>
        </tr>
        <tr >
          <td class="half-width">Total PDP inmates held in other jurisdictions</td>
          <td>{{ censusData.ojMale +  censusData.oocRothMale + censusData.oocCecMale + censusData.oocLehighMale + censusData.oocJuvMale + censusData.oocDelMale +  censusData.oocStateDocMale | rmZero }}</td>
          <td>{{ censusData.ojFemale +  censusData.oocRothFemale + censusData.oocCecFemale + censusData.oocLehighFemale + censusData.oocJuvFemale + censusData.oocDelFemale +  censusData.oocStateDocFemale | rmZero }}</td>
          <td>{{ censusData.ojTotal +  censusData.oocRothTotal + censusData.oocCecTotal + censusData.oocLehighTotal + censusData.oocJuvTotal + censusData.oocDelTotal +  censusData.oocStateDocTotal | rmZero }}</td>
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
    
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";

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
        return "-";
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

table tr td:not(:first-child) {
  font-weight: bold;
}

table {
  margin-bottom: 5rem;
}
</style>