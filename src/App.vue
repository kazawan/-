

<template>
  <div class="papper">
    <template v-for="p in  papperList">
      <input class="p1" type="text" placeholder="Plase input somethine" onfocus="this.placeholder='Please...'" onblur="this.placeholder='Plase input somethine'"
       v-model="p.content"  @keydown.enter="createP" @keydown.esc="cancelP"  @keyup="titleCheck" />
    </template>
    <input class="p1" type="text" placeholder="Plase input somethine" onfocus="this.placeholder='Please...'" onblur="this.placeholder='Plase input somethine'"
       v-model="pText"  @keydown.enter="createP" @keydown.esc="cancelP"  @keyup="titleCheck" />
    
  </div>

</template>

<script>
// const  titleType = {
//   ##:"h1"
// }

export default {
  
  data() {
    return {
      pText: '',
      papperList :[],
      eidting:true
    

    }
  },
  methods: {
    createP(){
      // console.log('createP')
      // console.log(this.pText)
      this.papperList.push({content: this.pText})
      this.pText = ''
      console.log(this.papperList)
      
    },
    cancelP(){
      // console.log('cancelP')
      this.pText = ''
    },
    titleCheck(){
      console.log('titleCheck')
      if(this.pText == '##'){
        console.log('h1')
      }
    },
    eidt(){
      this.eidting = !this.eidting
    }
  },
  
}
</script>





<style scoped>

root{
  --main:#303133
}
.papper {
  width: 100%;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.p1 {
  width: 100%;
  
  border: 0ch;
  background-color: #F0F2F5;
  caret-color: #A8ABB2;
  outline: none;
  font-family: "Noto Sans SC";
  font-weight: 600;
  color: var(--main);
  
}

.p1:hover {
  border-bottom: 1px solid #fdfdfd00;
}
</style>



