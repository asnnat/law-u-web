<script setup>
import { onMounted } from "vue";

//Vue Material Kit 2 components
import MaterialAvatar from "@/components/MaterialAvatar.vue";
import MaterialButton from "@/components/MaterialButton.vue";

// image
// import profilePic from "@/assets/img/bruce-mars.jpg";
import profilePic from "@/assets/img/law-u-mmm.png";

// material-input
import setMaterialInput from "@/assets/js/material-input";
onMounted(() => {
  setMaterialInput();
});
</script>
<template>
  <section class="py-sm-7 py-5 position-relative">
    <div class="container">
      <div class="row">
        <div class="col-12 mx-auto">
          <div class="mt-n8 mt-md-n9 text-center">
            <div class="blur-shadow-avatar">
              <MaterialAvatar
                size="xxl"
                class="shadow-xl position-relative z-index-2"
                :image="profilePic"
                alt="Avatar"
              />
            </div>
          </div>
          <div class="row py-7">
            <div
              class="col-lg-7 col-md-7 z-index-2 position-relative px-md-2 px-sm-5 mx-auto"
            >
              <div
                class="d-flex justify-content-between align-items-center mb-2"
              >
                <h3 class="mb-0">LAW-U รออยู่</h3>
                <div class="d-block">
                  <a href="https://line.me/ti/p/%40644ozljh" target="_blank">
                    <MaterialButton
                    class="text-nowrap mb-0"
                    variant="outline"
                    color="success"
                    size="sm"
                    >add Line</MaterialButton
                  >
                  </a>
                </div>
              </div>
              <!-- <div class="row mb-4">
                <div class="col-auto">
                  <span class="h6 me-1">9</span>
                  <span>Posts</span>
                </div>
                <div class="col-auto">
                  <span class="h6 me-1">7</span>
                  <span>Followers</span>
                </div>
                <div class="col-auto">
                  <span class="h6 me-1">10</span>
                  <span>Friends</span>
                </div>
              </div> -->
              <p class="text-lg mb-0">
                ที่ปรึกษาและให้คำแนะนำด้านกฎหมายเกี่ยวกับความรุนแรงงทางเพศ พร้อมให้คำปรึกษา 24 ชั่วโมง ภายใต้มาตรา 276, 277, 278 และ 279 แห่งประมวลกฎหมายอาญาช่วยให้คุณเข้าใจสิทธิและทางเลือกตามกฎหมาย ค้นหาสถานีตำรวจและโรงพยาบาลที่ใกล้ที่สุดและช่วยรักษาความเป็นส่วนตัวของบทสนทนา
                <br /><a
                  href="https://www.facebook.com/lawuthailand"
                  target="_blank"
                  class="text-success icon-move-right"
                  >อ่านเพิ่มเติม
                  <i class="fas fa-arrow-right text-sm ms-1"></i>
                </a>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
