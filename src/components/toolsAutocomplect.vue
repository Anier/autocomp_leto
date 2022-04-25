<template>
  <div class="ac" :id="id">
    <div class="ac-wrapper">
      <input type="text" class="ac-input" v-model.trim="text" @click="idx==null" v-on:keydown.enter="keyEnter()"
             v-on:keydown.down="keyDown()" v-on:keydown.up="keyUp()">
      <div class="ac-items" v-if="selectedList.length>0">
        <div v-for="(t,i) in selectedList" :key="i" :class="'ac-item '+((i == idx) ? 'hovers':'')"
             @click="selectItem(i)">
          {{ t.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "toolsAutocomplect",
  props: {
    items: Array,
    css: Array,
    id: String
  },
  watch: {
    text() {
      this.searching();
    },

  },
  data() {
    return {
      text: '',
      param: {
        minChar: 1,
      },
      selectedList: [],
      idx: null,
    }
  },
  mounted() {
    // let d = document.querySelector('.ac-wrapper');
    document.addEventListener('click', e => {
      let f = e.path.findIndex((j) => j.className == 'ac-wrapper');
      if (f < 0) this.selectedList = [];
    })
    this.put_css();
  },
  methods: {
    put_css() {
      for (let e of this.css) {
        let k = Object.keys(e);
        let els = document.querySelectorAll('#' + this.id + ' .' + k);
        console.log(els);
        if (els) {
          for (let css of Object.keys(e[k])) {
            for (let el of els) {
              console.log(el, css, e[k][css]);
              el.style[css] = e[k][css];
            }
          }
        }
      }

    },

    keyEnter() {
      if (this.idx !== null) {
        this.text = this.selectedList[this.idx].name;
        this.idx = null;
      } else {
        this.selectedList = [];
        alert('send data');
      }
    },
    keyDown() {
      if (this.selectedList.length > 0 && this.selectedList.length > this.idx + 1) {
        if (this.idx === null) this.idx = 0; else this.idx++;
      }
    },
    keyUp() {
      if (this.selectedList.length > 0 && this.selectedList.length >= this.idx + 1) {
        if (this.idx === 0) this.idx = null; else this.idx--;
      }
    },
    selectItem(i) {
      this.text = this.selectedList[i].name;
    },
    searching() {
      if (this.param.minChar <= this.text.length) {
        const runs = async () => {
          const sl = () => {
            return new Promise(resolve => {
              resolve(
                  this.selectedList = this.items.filter((e) => {
                    if (e.name.toLowerCase().includes(this.text.toLowerCase())) {
                      return e.name;
                    }
                  })
              )
            })
          }
          const putcss = () => {
            if (this.selectedList.length > 0) this.put_css();
          }
          return [await sl(), await putcss()];
        }

        runs();


      } else this.selectedList = [];
    }
  }
}
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.hovers {
  background-color: #eee;
  cursor: pointer;
}

.ac-wrapper {
  position: relative;
  z-index: 2;
  padding: 6px 6px 0px 6px;
  height: 40px;
}

.ac-input {
  padding: 3px 5px;
  border: 1px solid #666;
  font-family: "Roboto", sans-serif;
  font-size: 110%;
  width: 100%;
  background-color: #fefefe;
}

.ac-items {
  background-color: rgba(255, 255, 255, 1);
  border-left: 1px solid #ccc;
  border-right: 1px solid #ccc;
  border-bottom: 1px solid #ccc;
}

.ac-item {
  padding: 2px 5px;
  font-size: 100%;
  border-bottom: 1px dotted #bbb;
  text-align: start;
}

.ac-item:hover {
  background-color: #eee;
  cursor: pointer;
}

.ac-item:nth-last-child(1) {
  border-bottom: none;
  padding-bottom: 6px;
}


</style>