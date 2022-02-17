<template>
    <div class="cbox">
        <div class="ctitle">
            Order Summary 
        </div>
        <div class="sum-item">
            <span>Items</span>
            <span class="float-right" v-text="data.itotal.toFixed(2)"></span>
        </div> 
        <div class="sum-item">
            <span>Tax</span>
            <span class="float-right" v-text="data.tax.toFixed(2)"></span>
        </div>
        <div class="sum-item">
            <span>Shipping</span>
            <span class="float-right" v-text="data.shipping.toFixed(2)"></span>
        </div>
        <div class="sum-item">
            <span>Sub Total</span>
            <span class="float-right" v-text="data.subtotal.toFixed(2)"></span>
        </div> 
        <button class="cbtn w-100 p-2 h-auto" @click="handleClick">
            <span>Buy now</span>
        </button>
    </div>
</template>
<script>
export default {
    name: 'SummaryBox',
    props: {
      data: Object,
      completed: Boolean
    },
    methods: {
      handleClick() {
        this.$emit('completed');
      }
    }
}
</script>
<style lang="scss">
.sum-item {
    padding: 10px 20px 10px 15px;
    max-height: 120px;
    display: block;
    align-items: center;
}
.float-right {
    float: right;
}
</style>