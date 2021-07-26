<template>
    <div class="item">
        <input type="checkbox" @change="updateCheck()" v-model="item.completed">
        <span :class="[item.completed ? 'completed' : '', 'itemtext']">{{item.name}}</span>
        <button @click="removeItem()" class="removeitem">
            <font-awesome-icon icon="trash"/>
        </button>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    props: ['item'],
    methods: {
        updateCheck() {
            axios.put('api/item/' + this.item.id, {item: this.item})
            .then(res => {
                if(res.status == 200)
                    this.$emit('itemchanged');
            })
            .catch(err => console.error(err));
        },
        removeItem() {
            axios.delete('api/item/'+this.item.id)
            .then(res => {
                if(res.status == 200)
                    this.$emit('itemchanged');
            })
            .catch(err => console.error(err));
        }
    }
}
</script>

<style scoped>
.item {
    display: flex;
    justify-content: center;
    align-content: center;
}

.completed {
    text-decoration: line-through;
    opacity: 0.8;
}

.itemtext {
    width: 100%;
    margin-left: 20px;
}

.removeitem {
    background-color: #e6e6e6;
    border: none;
    color: red;
    outline: none;
    cursor: pointer;
}
</style>