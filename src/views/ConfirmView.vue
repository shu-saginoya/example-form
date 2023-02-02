<script setup lang="ts">
import { ref, inject } from "vue";
import type { CustomerInfo, PostData } from "@/interfaces";

// Layout components
import LyCont from "@/components/LyCont.vue";

// Block components
import BlContsUnit from "@/components/BlContsUnit.vue";
import BlFieldset from "@/components/BlFieldset.vue";
import BlInputGroup from "@/components/BlInputGroup.vue";
import BlHorizBtnList from "@/components/BlHorizBtnList.vue";
import ElTextarea from "@/components/ElTextarea.vue";

// Elemnt components
import ElBtn from "@/components/ElBtn.vue";

const customerInfo = inject<CustomerInfo>("customerInfo");
const postData = inject<PostData>("postData");

const name = ref(postData ? postData.postName : "");
const department = ref(postData ? postData.postDepartment : "");
const businessType = ref(customerInfo ? customerInfo.businessType : "");
const postalCode = ref(customerInfo ? customerInfo.postalCode : "");
const address = ref(postData ? postData.postAddress : "");
const tel = ref(customerInfo ? customerInfo.tel : "");
const fax = ref(customerInfo ? customerInfo.fax : "");
const email = ref(customerInfo ? customerInfo.email : "");
const dm = ref(customerInfo ? customerInfo.dm : "");
const magazines = ref(postData ? postData.postMagazines : "");
const remarks = ref(customerInfo ? customerInfo.remarks : "");
</script>

<template>
  <LyCont>
    <BlContsUnit>
      <h2 class="el_lv2heading">入力内容の確認</h2>
      <form method="post" action="/">
        <BlFieldset>
          <BlInputGroup
            label="ご契約者名"
            id="post-name"
            type="text"
            required
            v-model="name"
            readonly
          ></BlInputGroup>
          <BlInputGroup
            label="部署・ご担当者様"
            id="post-department"
            type="text"
            v-model="department"
            readonly
          ></BlInputGroup>
          <BlInputGroup
            label="業種"
            id="post-business-type"
            type="text"
            required
            v-model="businessType"
            readonly
          ></BlInputGroup>
          <BlInputGroup
            label="郵便番号"
            id="post-postal-code"
            type="text"
            required
            v-model="postalCode"
            readonly
          ></BlInputGroup>
          <BlInputGroup
            label="ご住所"
            id="post-address"
            type="text"
            required
            v-model="address"
            readonly
          ></BlInputGroup>
          <BlInputGroup
            label="電話番号"
            id="post-tel"
            type="text"
            required
            v-model="tel"
            readonly
          ></BlInputGroup>
          <BlInputGroup
            label="FAX番号"
            id="post-fax"
            type="text"
            v-model="fax"
            readonly
          ></BlInputGroup>
          <BlInputGroup
            label="メールアドレス"
            id="post-email"
            type="text"
            required
            v-model="email"
            readonly
          ></BlInputGroup>
          <BlInputGroup
            label="DMのご希望"
            id="post-dm"
            type="text"
            v-model="dm"
            readonly
          ></BlInputGroup>
          <BlInputGroup
            v-for="(magazine, index) in magazines"
            :key="`magazine${index}`"
            :label="`ご希望の新聞・雑誌${index + 1}`"
            :id="`post-magazines${index}`"
            type="text"
            :required="index === 0"
            :model-value="magazine"
            readonly
          ></BlInputGroup>
          <BlInputGroup label="備考欄">
            <ElTextarea id="post-remarks" rows="5" v-model="remarks" readonly>
            </ElTextarea>
          </BlInputGroup>
          <BlHorizBtnList>
            <li>
              <ElBtn color="gray" @click="$router.push('/')">修正する</ElBtn>
            </li>
            <li>
              <ElBtn type="submit">送信する</ElBtn>
            </li>
          </BlHorizBtnList>
        </BlFieldset>
      </form>
    </BlContsUnit>
  </LyCont>
</template>