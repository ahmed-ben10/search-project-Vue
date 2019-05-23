<template>
    <div id="search-container">
        <label id="search-label" for="search">Search</label>
        <input id="search-bar" type="search" 
        v-model="searchText" 
        @keydown="$emit('searched',searchText) " 
        placeholder="Search">
    </div>
</template>

<script>
export default {
    name:"search-bar",
    data:()=>{
        return{
            searchText:''
        }
    },
}
</script>

<style>

</style>
