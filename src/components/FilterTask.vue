<template>
  <div>
    <div>
        <button @click="updateFilter('all')" :class="current === 'all' ? 'active' :''">Hepsi</button>
        <button @click="updateFilter('completed')" :class="current === 'completed' ? 'active' :''">Tamamlandı</button>
        <button @click="updateFilter('continue')" :class="current === 'continue' ? 'active' :''">Devam Ediyor</button>
      </div>
  </div>
</template>

<script>
export default {
    emits:['updateFilter'],
    props:['current'],
    methods:{
        updateFilter(filter){
            this.$emit('updateFilter',filter)
        }
    }
}
</script>

<style>
button{
    margin: 5px;
    padding: 10px;
    border: none;
    border-radius: 20px;
    font-size: 12px;
    font-weight: bold;
    background: bisque;
    color: gray;
    cursor: pointer;
    text-transform: uppercase;
    letter-spacing: 1px;
  }
  button:hover{
    color: black;
  }
  .active{
    color: black;
  }
</style>