<template>
  <div>
    <nav>
      <router-link class="link active"  to="/">Yapılacaklar Listesi</router-link> 
      <router-link  class="link" to="/addTask">Yeni Görev Ekle</router-link> 
    </nav>
    <router-view/>
  </div>
</template>



<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;

}
body{
  background: ghostwhite;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  width: 100%;
  margin: 0 auto;

}

nav{
  display: flex;
  justify-content: center;
  margin: 40px 0px;
}
a{
  margin: 0px 20px;
  text-decoration: none;
  color: gray;
  font-size: 18px;
  cursor: pointer;
}
a.router-link-active{
  border-bottom: 2px solid green;
}
</style>
