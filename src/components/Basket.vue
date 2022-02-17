<template>
    <div class="cbox">
        <div class="ctitle">
            Basket
        </div>
        <div class="item" v-for="item in data" :key="item.id">
            <div class="quantity">
                <button class="cbtn" @click="update(item, 'add')">
                    <span>+</span>
                </button>
                <span class="item_quantity">{{ item.quantity }}</span>
                <button class="cbtn" @click="update(item, 'sub')">
                    <span>-</span>
                </button>
            </div>
            <div class="description">
                <span v-text="item.title"></span>
            </div> 
            <div class="total-price">£{{ item.price.toFixed(2) }}</div>
            <button class="btn delete" @click="remove(item)">
                <span aria-hidden="true">&times;</span>
            </button>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Basket',
    props: {
        data: Array,
        update: Function,
        remove: Function
    }
}
</script>
<style lang="scss">
.item {
    padding: 10px 5px;
    max-height: 120px;
    display: flex;
    align-items: center;
}
.total-price {
    width: 83px;
    text-align: center;
    font-size: 16px;
    color: white;
    font-weight: 300;
    background-color: rgb(13, 110, 253);
    border-radius: 12px;
    height: 25px;
    margin-left: 12px;
}
.quantity {
    width: 85px;
}
.item_quantity {
    font-size: 1.5rem;
    text-align: center;
    width: 32px;
    font-size: 16px;
    color: #43484D;
    font-weight: 300;
    margin-left: 5px;
    margin-right: 5px;
}
.delete {
    padding: 0.5rem 0.5rem;
}
</style>