<template>
    <div class="todolistcontainer">
        <div class="heading">
            <h2>Laravel Todo List</h2>
            <add-item-form />
        </div>
        <list-view :items="this.items" v-on:reloadlist="getList()"/>
    </div>
</template>

<script>
import AddItemForm from './AddItemForm';
import ListView from './ListView';
import axios from 'axios';

export default {
    components : {
        AddItemForm,
        ListView
    },
    data: function(){
        return {
            items: []
        }
    },
    methods: {
        getList(){
            axios.get('api/items')
            .then(res => this.items = res.data)
            .catch(err => console.error(err));
        }
    },
    created() {
        this.getList();
    }
}
</script>

<style scoped>
.todolistcontainer {
    width: 50%;
    margin: 0 auto;
}

.heading {
    padding: 5px;
    text-align: center;
    background-color: #c2c2c2;
}
</style>