<template>
  <div class="container_cardItem">
    <cardItem ref="cardItemRef" :list = "productsStore.all" @updateList='updateList'>
      <span>我是默认插槽</span>
      <template #title>
        <h1>我是具名插槽</h1>
      </template>
      <template #footer="{ scope }">
        <footer>作用域插槽——姓名：{{ scope.name }}，年龄{{ scope.age }}</footer>
      </template>
    </cardItem>
  </div>
</template>

<script setup lang="ts">
  import cardItem from './card.vue'
  // import {nextTick,ref} from 'vue'  使用了 unplugin-auto-import 可以注释
  import { useProductsStore } from "@/store/products";
  const productsStore = useProductsStore();
  // 加载所有数据
  productsStore.loadAllProducts();
  interface IProduct {
      id: number;
      title: string;
      price: number;
      inventory: number;
  }
  const updateList = (list: IProduct[]) => {
      // console.log(list)
      productsStore.all = list
  }  


  // 子组件ref
  // const childRef = ref('cardItemRef')
  const cardItemRef = ref();
  // console.log(cardItemRef,'111')
  // nextTick
  nextTick(() => {
    // 获取子组件name
    console.log(cardItemRef.value.name)
    // 执行子组件方法
    cardItemRef.value.changeName
  })  
</script>

<style lang="scss" scoped>
 .container_cardItem{
     padding: 20px;
 }
</style>