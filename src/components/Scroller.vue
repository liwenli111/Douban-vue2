<template>
  <div class="scroller">
    <div class="header">
      <h2>{{ title }}</h2>
      <a href="#">更多</a>
    </div>
    <div class="content">
      <slot name="promItem"></slot>
      <ul class="hasCover" v-if="type === 'hasCover' ">
        <li v-for="item in items">
          <router-link :to=" 'subject/' + item.id" append>
            <img v-if="item.images" :src="item.images.large" alt="">
            <span class="title">{{ item.title }}</span>
            <rating v-if="item.rating" :rating="item.rating">
            </rating>
          </router-link>
        </li>
      </ul>
      <ul class="onlyString" v-if="type === 'onlyString' ">
        <li v-for="item in items" style="border-color: #FFAC2D">
          <a :href="item.href" v-if="!item.line" :style="{color: item.color}">{{ item.title }}</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import Rating from './Rating.vue'

export default {
    components: {
      Rating
    },
    props: {
      title: {
        type: String,
        required: true
      },
      items: {
        type: Array,
        default: [],
        required: false
      },
      type: {
        type: String,
        default: 'hotCover'
      }
    }
  }
</script>

<style lang="scss" scoped>
.scroller {
  padding-top: 1rem;
  .header {
    display: flex;
    justify-content: space-between;
    height: 2.6rem;
    line-height: 2.6rem;

    h2{
      margin-left: 1.6rem;
    }

    a {
      margin-right: 1.6rem;
      font-size: 1.44rem;
      color: #42bd56;
    }
  }

  .hasCover {
    display: flex;
    overflow-x: auto;
    overflow-y: hidden;
    white-space: nowrap;
    text-align: center;
    padding-right: 1rem;
    margin-top: 1rem;

    .title {
      display: block;
      max-width: 100%;
      margin-top: 1rem;
      line-height: 1.6rem;
      font-size: 1.6rem;
      color: #111;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
      word-wrap: normal;
    }

    li {
      display: inline-block;
      width: 10rem;
      margin-left: 1rem;
    }

    li:first-child {
      padding-left: 0.8rem;
      /*overflow: hidden;*/
    }

    li:last-child {
      padding-right: 2rem;
    }

    img {
      height: 15rem;
    }
  }

  .onlyString {
    overflow-x: auto;
    white-space: nowrap;

    li {
      display: inline-block;
      margin: 0 2rem 0.8rem 1.6rem;
      font-size: 1.6rem;
      border: 0.1rem solid rebeccapurple;
      border-radius: 0.4rem;
      vertical-align: middle;
    }

    a {
      height: 4rem;
      line-height: 4rem;
      padding: 0 2.4rem;
      letter-spacing: 0.16rem;
      overflow: auto;
      display: block;
      text-align: center;
    }

    li:empty {
      width: 100%;
      display: block;
      height: 0.1rem;
      border: 0;
      margin: 0;
    }

  }
}
</style>
