<template>
  <div>
    <Header :title="'我的购物车'" background="pink" color="green"></Header>
    <Goods v-for="item in list" :key="item.id" :list="item"></Goods>
    <Footer :arr="list" @changeAll="allFn"></Footer>
  </div>
</template>

<script>
import Header from '@/components/MyHeader.vue'
import Goods from '@/components/MyGoods.vue'
import Footer from '@/components/MyFooter.vue'
export default {
  components: { Header, Goods, Footer },
  data() {
    return {
      list: [],
    }
  },

  created() {
    this.$axios({
      url: 'api/cart'
    }).then(res => {
      this.list = res.data.list
    })
  },
  methods: {
    allFn(val) {
      this.list.forEach(ele => ele.goods_state = val)
    }
  },
}
</script>

<style>
</style>