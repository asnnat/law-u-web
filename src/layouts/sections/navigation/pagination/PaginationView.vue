<script setup>
import { onMounted } from "vue";

// Sections components
import BaseLayout from "../../components/BaseLayout.vue";
import View from "../../components/View.vue";

// Pagination page components
import PaginationSimple from "./components/PaginationSimple.vue";

// Pagination page components codes
import { paginationSimpleCode } from "./components/codes";

//nav-pills
import setNavPills from "@/assets/js/nav-pills";

import { useRoute } from 'vue-router';
import metadata from "./../../../../assets/json/metadata.json";

const route = useRoute();
const data = metadata;

//hook
onMounted(() => {
  setNavPills();
});
</script>

<template>
  <BaseLayout title="คำพิพากษาศาลฎีกาที่เกี่ยวข้อง"
    :breadcrumb="[{ label: 'หน้าแรก', route: '/' }, { label: 'คำพิพากษาศาลฎีกาที่เกี่ยวข้อง' }]"
    :data="data"
    :dekaId="route.params.id">
    <View title="คำพิพากษาศาลฎีกาที่ " :code="paginationSimpleCode" id="pagination-simple" :data="data" :dekaId="route.params.id">
      <PaginationSimple :data="data" :dekaId="route.params.id"/>
    </View>
  </BaseLayout>
</template>
