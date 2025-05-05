<script lang="ts">
import { defineComponent, ref } from 'vue';
import { imagesContainer } from 'src/assets/images/Images'

export default defineComponent({
  setup() {
    const textPrivacy = ref('Política de privacidade')
    const textDireitos = ref('Todos os direitos reservados por FireBeauty')

    return {
      imagesContainer,
      textPrivacy,
      textDireitos
    }
  }
})


</script>

<template>
  <q-layout view="hhh Lpr lFf">
    <q-header elevated class="bg-white header">
      <div class="header-content">
        <img :src="imagesContainer.logo" alt="Logo FireBeauty" class="logo"
          style="width: 141px; height: 49px; margin-bottom: 10px;">
      </div>
    </q-header>

    <q-page-container style="padding: 0;">
      <router-view v-slot="{ Component }">
        <keep-alive>
          <component :is="Component" />
        </keep-alive>
      </router-view>
    </q-page-container>


  </q-layout>
</template>

<style lang="scss" scoped>
.header {
  height: 70px;

  &-content {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>