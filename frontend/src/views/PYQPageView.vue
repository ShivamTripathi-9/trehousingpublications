<template>
  <Header />
<PYQup/>

  <!-- <PyqRightSection/> -->
  <!-- <TreFourZero /> -->
  <PyqOverview />
  <TextTable/>
  

  <!-- <Notification /> -->
  <!-- <PyqRightSection/> -->
   
  <BiharSyllabusComponent/>

  <PyqSyPdf />

  <Footer />
</template>

<script>
import Header from "@/components/Homepage/HeaderSec.vue";
import Footer from "@/components/Homepage/FooterSec.vue";


// import Notification from "@/components/PYQ/NotificationPanel.vue";
import PyqSyPdf from "@/components/PYQ/PyqSyPdf.vue";
// import BiharSyllabusComponent from "@/components/PYQ/BiharSyllabusComponent.vue";


// import Notification from "@/components/PYQs/NotificationPanel.vue";
// import PyqSyPdf from "@/components/PYQs/PyqSyPdf.vue";

// import Notification from "@/components/PYQ/NotificationPanel.vue";
// import PyqSyPdf from "@/components/PYQ/PyqSyPdf.vue";
import TextTable from "@/components/PYQ/TextTable.vue";
// import TreFourZero from "@/components/PYQ/TreFourZero.vue";
import PyqOverview from '@/components/PYQ/PyqOverview.vue';

// import PyqRightSection from "@/components/PYQ/PyqRightSection.vue";

import PYQup from "@/components/PYQ/PYQup.vue"

// import BiharSyllabusComponent from "@/components/PYQ/BiharSyllabusComponent.vue";

export default {
  name: "SyllabusView",
  components: {
    Header,
    PYQup,

    // TreFourZero,

    // PyqRightSection,
    // Notification,
    PyqSyPdf,

    // BiharSyllabusComponent,


    TextTable,
    PyqOverview,


    Footer,
  },
};
</script>

<style></style>
