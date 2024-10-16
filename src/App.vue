<script> // Барышников М.В.
  export default{
    data(){
      return{
        name:'',
        list:[]
		   	 }
    },
    methods:{
      test(){
        this.list.push(this.name);
        
      },
      sor(){
         this.list.sort();
        },
        dell(){
          this.list=0;
        }

    }
  }
</script>
<template>

  <h1>Мои задачи</h1>
  <div class="container">
    <div class="header">
      <input type="text" placeholder="Введи задачу" class="in" v-model="name">
         <button :disabled="!name" class="btn" @click="test();">Добавить</button>
      </div>
    <div class="content">
      <div class="task" v-for="x in list">
        <input type="radio" name="task1" class="in_r"><p class="text_task">{{ x }}</p>
      </div>
    </div>
    <div class="footer">
      <hr>
      <button  @click="dell();">Удалить всё</button><button @click="sor();">Сортировать</button>
      </div>
  </div>

  <!-- <input type="text" > 
  <button v-if="name!=''" >КНОПКА</button>
  <button v-if=" list.length>1" @click="sor();">сортировка</button>
  <ul>
    <li v-for="x in list"> {{ x }}</li>
  </ul> -->
</template>
<style scoped>

</style>