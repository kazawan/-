

<template>
  <div class="papper">
    <template v-for="p in  papperList" :key="p.id">
      <input class="p1" :id="p.id" type="text" placeholder="" onfocus="this.placeholder='...'"
        onblur="this.placeholder=''" v-model="p.content" @keydown.enter="nextLine(p)" @keydown.esc="cancelP"
        @keydown.up="moveup(p)" @keydown.down="movedown(p)" @keydown.delete="del(p)" />
    </template>
    <input class="p1" id="input_1" type="text" :placeholder="INPUT_placeholder" onfocus="this.placeholder='...'"
      onblur="this.placeholder=''" v-model="pText" @keydown.enter="createP" @keydown.esc="cancelP"
      @keydown.up="input_1moveup()" />

  </div>

</template>

<script>
let id = 0;

export default {
  data() {
    return {
      pText: '',
      papperList: [],
      INPUT_placeholder: 'Plase input somethine',
    }
  },
  methods: {
    createP() {
      this.papperList.push({
        content: this.pText,
        id: id++
      })
      this.pText = ''
      this.resetID()
    },
    cancelP() {
      // console.log('cancelP')
      this.pText = ''
    },
    nextLine(p) {
      if (p.id == this.papperList.length - 1) {
        document.getElementById('input_1').focus()
        return
      } else {
        let start = document.getElementById(p.id).selectionStart
        const index = this.papperList.findIndex(item => item.id == p.id) + 1
        this.papperList.splice(index, 0, { content: p.content.substring(start), id: id++ })
        this.resetID()
        document.getElementById(p.id + 1).focus()
        p.content = p.content.substring(0, start)
        console.log(this.papperList)
      }

    },
    resetID() {
      let count = 0;
      this.papperList.forEach(item => item.id = count++)
    },
    moveup(p) {
      this.resetID()
      if (p.id == 0) {
        return
      }
      document.getElementById(p.id - 1).focus()
    },
    movedown(p) {
      this.resetID()
      if (p.id == this.papperList.length - 1) {
        document.getElementById('input_1').focus()
        return
      } else {
        document.getElementById(p.id + 1).focus()
      }
    },
    input_1moveup() {
      this.resetID()
      if (this.papperList.length > 0) {
        document.getElementById(this.papperList.length - 1).focus()
      }
      return
    },
    del(p) {
      if(p.id == 0){
        return
      }
      if (p.content.length > 0 && document.getElementById(p.id).selectionStart != 0) {
        console.log('還有内容')
      } else if (p.content.length > 0 && document.getElementById(p.id).selectionStart == 0) {
        console.log('在盡頭了')
        const index = this.papperList.findIndex(item => item.id == p.id)
        let start = document.getElementById(p.id).selectionStart
        

        let content = this.papperList[index].content
        this.papperList.splice(index - 1, 1, { content: this.papperList[index - 1].content + content + ' ' })
        this.papperList.splice(index, 1)
        this.resetID()
        // this.moveup(p)
        
        let targetContentLength = this.papperList[index - 1].content.length
        let tar = targetContentLength - p.content.length
        document.getElementById(index - 1).setSelectionRange(tar, tar)
        document.getElementById(index - 1).focus()



      } else {
        if (this.papperList.length === 0) {
          return
        } else {
          const index = this.papperList.findIndex(item => item.id == p.id)
          this.papperList.splice(index, 1)
          this.papperList.splice(index - 1, 1, { content: this.papperList[index - 1].content + ' ' })
          this.resetID()
          this.moveup(p)
          console.log(this.papperList)
          console.log('刪除這一行')
        }

      }
    }


  },
  mounted() {
    let input_1 = document.getElementById('input_1')
    // console.log(this.pText.length)
    // input_1.setSelectionRange(this.pText.length-1,this.pText.length-1)
    input_1.focus();

  }


}
</script>





<style scoped>
root {
  --main: #303133
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



