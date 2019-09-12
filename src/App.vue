<template>
  <div id="app">
    <h1>Группы вида &lt;&#x2124;<sub>m</sub>, +> </h1>
    <div class="tables">
      <CayleyTable :key="i" v-for="i in 6" :m="i+2" operator="+"></CayleyTable>
    </div>
    <h1>Группы вида &gt;&#x2124;<sup>*</sup><sub>m</sub>, *> </h1>
    <div class="tables">
      <CayleyTable :key="i" v-for="i in 6" :m="i+4" operator="*" coprime></CayleyTable>
    </div>

  </div>
</template>

<script>
import CayleyTable from './components/CayleyTable/CayleyTable'

export default {
  name: 'app',
  components: {
    CayleyTable
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;

}
  .cayley-table {
    margin: 30px;
  }
  .tables {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
  h1 {
    display: block;
    text-align: center;
  }
</style>
