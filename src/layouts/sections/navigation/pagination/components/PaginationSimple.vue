<script setup>
//Vue Material Kit 2 components
import MaterialPagination from "@/components/MaterialPagination.vue";
import MaterialPaginationItem from "@/components/MaterialPaginationItem.vue";

import { ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();
const id = route.params.id

const pageNumberInput = ref();

const props = defineProps({
  data: {
    type: Object,
    required: true,
  },
  dekaId: {
    type: String,
    required: true
  }
});

const dataLength = () => {
  return props.data ? Object.keys(props.data).length.toString() : 'loading';
};


const handleItemClick = (label) => {
  const currentId = parseInt(label);

  router.push({
    name: 'navigation-pagination',
    params: { id: label }
  });
};

const handlePrevClick = (label) => {
  const currentId = parseInt(label);

  router.push({
    name: 'navigation-pagination',
    params: { id: currentId - 1 }
  });
};

const handleNextClick = (label) => {
  const currentId = parseInt(label);

  router.push({
    name: 'navigation-pagination',
    params: { id: currentId + 1 }
  });
};

const handleRandomClick = () => {
  const randomNumber = Math.floor(Math.random() * parseInt(dataLength())) + 1;

  router.push({
    name: 'navigation-pagination',
    params: { id: randomNumber }
  });
};

const navigateToPage = () => {
  let inputText = pageNumberInput.value;

  if (!inputText.includes('/')) {
    console.log(inputText)
    alert('กรุณากรอกข้อมูลในรูปแบบ XXXX/YEAR');
    return;
  }

  pageNumberInput.value = null

  if (props.data) {
    let foundIndex = null;

    for (const index in props.data) {
      const item = props.data[index];

      if (item['header'].includes(inputText)) {
        console.log('Item found:', item);

        foundIndex = (parseInt(index) + 1).toString();
        break;
      }
    }

    if (foundIndex !== null) {
      router.push({
        name: 'navigation-pagination',
        params: { id: foundIndex }
      });
    } else {
      alert('ไม่พบข้อมูลที่ค้นหา');
    }
  }
};

</script>

<template>
  <section class="py-5">
    <div class="container">
      <div class="row">
        <div class="col-lg-4 col-md-6 col-sm-12 mx-auto">
          <!-- <MaterialPagination :style="{ marginLeft: '80px' }"> -->
          <MaterialPagination style="display: flex; justify-content: center;">
            <!-- Previous button -->
            <MaterialPaginationItem v-if="props.dekaId === '1'" prev disabled />
            <MaterialPaginationItem v-if="props.dekaId > '1'" prev @click="handlePrevClick(props.dekaId)" />

            <!-- First pagination item -->
            <MaterialPaginationItem @click="handleItemClick('1')" :active="props.dekaId === '1'" label='1' />

            <!-- Middle pagination items -->
            <template v-if="props.dekaId <= 3">
              <MaterialPaginationItem v-for="pageNumber in [2, 3, 4]" :key="pageNumber"
                @click="handleItemClick(pageNumber.toString())" :active="props.dekaId === pageNumber.toString()"
                :label="pageNumber.toString()" />
            </template>
            <template v-else-if="props.dekaId <= parseInt(dataLength()) - 3">
              <MaterialPaginationItem v-for="pageNumber in [props.dekaId - 1, props.dekaId, parseInt(props.dekaId) + 1]"
                :key="pageNumber" @click="handleItemClick(pageNumber.toString())"
                :active="props.dekaId === pageNumber.toString()" :label="pageNumber.toString()" />
            </template>
            <template v-else>
              <MaterialPaginationItem
                v-for="pageNumber in [parseInt(dataLength()) - 3, parseInt(dataLength()) - 2, parseInt(dataLength()) - 1]"
                :key="pageNumber" @click="handleItemClick(pageNumber.toString())"
                :active="props.dekaId === pageNumber.toString()" :label="pageNumber.toString()" />
            </template>

            <!-- Last pagination item -->
            <MaterialPaginationItem v-if="props.dekaId <= parseInt(dataLength())" @click="handleItemClick(dataLength())"
              :active="props.dekaId === dataLength()" :label="dataLength()" />

            <!-- Next button -->
            <MaterialPaginationItem v-if="parseInt(props.dekaId) < parseInt(dataLength())" next
              @click="handleNextClick(props.dekaId)" />
            <MaterialPaginationItem v-if="parseInt(props.dekaId) === parseInt(dataLength())" next disabled />

            <!-- Random button -->
            <MaterialPaginationItem @click="handleRandomClick()" random />
          </MaterialPagination>
        </div>
      </div>
      <div class="row">
        <div class="col-lg-4 col-md-6 col-sm-12 mx-auto">
          <!-- Input deka number -->
          <div style="display: flex; justify-content: center;">
            <input id="pageNumber" type="text" v-model="pageNumberInput" placeholder="XXXX/YEAR">
            <button @click="navigateToPage">ค้นหา</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>