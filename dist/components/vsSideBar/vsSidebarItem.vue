<template lang="html">
  <li @click="clickItem" :class="{'con-tag':vsTag,'active-item':vsActive}" class="vs-component vs-sidebar-item">
    <router-link
    :title="reduce?$slots.default[0].text:null"
    v-bind="$attrs"
    v-on="$listeners"
    v-if="to"
    :to="to">
    <span class="con-text-span">
      <i v-if="vsIcon" class="material-icons">
        {{vsIcon}}
      </i>
      <i v-if="vsIconReduce" class="material-icons only-reduse">
        {{vsIconReduce}}
      </i>
      <span class="textx_span">
        <slot/>
      </span>
    </span>

      <span :title="reduce?vsTag:null" v-if="vsTag" class="vs-tagx">{{vsTag}}</span>
  </router-link>

  <template v-else-if="vsSlot">
    <slot/>
  </template>

    <a
    v-else
    :title="reduce?$slots.default[0].text:null"
    v-bind="$attrs"
    v-on="$listeners"
    :href="href">
    <span class="con-text-span">
      <i v-if="vsIcon" class="material-icons">
        {{vsIcon}}
      </i>
      <i v-if="vsIconReduce" class="material-icons only-reduse">
        {{vsIconReduce}}
      </i>
      <span class="textx_span">
        <slot/>
      </span>
    </span>
    <span :title="reduce?vsTag:null" v-if="vsTag" class="vs-tagx">{{vsTag}}</span>
    </a>

  </li>
</template>

<script>
export default {
  name:'vs-sidebar-item',
  props:{
    to:{},
    href:{},
    vsIcon:{
      default:null,
      type:String
    },
    vsIconReduce:{
      default:null,
      type:String
    },
    vsSlot:{
      type:Boolean,
      default:false,
    },
    vsActive:{
      default:false,
      type:Boolean
    },
    vsTag:{
      default:null,
      type:[String,Number],
    }
  },
  data:()=>({
    reduce:false
  }),
  methods:{
    clickItem(){
      this.$parent.clickItem(this.vsActive)
    }
  }
}
</script>

<style lang="stylus">




@css{
  .vs-sidebar-item:after {
    background: rgb(var(--primary));
  }
}


.only-reduse
  display: none;
.vs-sidebar-item
  list-style: none;
  width: 100%;
  display: flex;
  align-items: center;
  cursor: pointer;
  position: relative;
  &:after
    content: ''
    left: 0px;
    top: 0px;
    height: 0%;
    position: absolute;
    width:4px;
    border-radius: 0px 6px 6px 0px;

    transition: all .3s ease;
    top: 50%;
    transform: translate(0,-50%);
  a
    color: rgba(0, 0, 0, 0.550);
    display: flex;
    align-items: center;
    padding: 8px;
    padding-left: 15px;
    width: calc(100% - 6px);
    margin-left: 3px;
    font-size: 15px;
    transition: all .2s ease
    text-decoration: none !important;
    .con-text-span
      display: flex;
      align-items: center;

    ../:not(.active-item)&:hover
      background: rgb(255, 255, 255);
      border-radius: 10px;
      z-index: 100

    .vs-tagx
      position: relative;
      z-index: 200;
      color: rgb(255, 255, 255);
      border-radius: 8px;
      padding-top: 0px;
      padding-bottom: 0px;
      font-size: 10px;
      padding-left: 5px;
      padding-right: 5px;
      font-weight: normal;
      box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.1)
    i.material-icons
      margin-right: 10px;
      font-size: 18px;
&.con-tag
  a
    justify-content: space-between !important;
    padding-right: 5px;
&.active-item
  background: rgb(248, 248, 248);

  a
    font-weight: bold;
  &:after
    height: 100% !important

@css{
  .vs-sidebar-item:not(.active-item) a:hover {
    color: rgb(var(--primary))
  }
  .vs-tagx {
    background: rgb(var(--primary));
  }
  .active-item a {
    color: rgb(var(--primary));
  }
}
</style>
