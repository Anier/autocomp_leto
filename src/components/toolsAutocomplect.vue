<template>
  <div class="ac" :id="id">
    <div class="ac-wrapper">
      <input type="text" class="ac-input" v-model.trim="text" @click="idx==null" v-on:keydown.enter="keyEnter()"
             v-on:keydown.down="keyDown()" v-on:keydown.up="keyUp()">
      <div class="ac-button" @click="putValueBack(); selectedList = []">send</div>
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
    id: String,
    datareturn: Function
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
      idx: -1,
    }
  },
  mounted() {
    /**
     * Enable mouse click tracking to close the popup list
     */
    document.addEventListener('click', e => {
      let f = e.path.findIndex((j) => j.className == 'ac-wrapper');
      if (f < 0) this.selectedList = [];
    })
    this.put_css();
  },
  methods: {
    putValueBack() {
      this.datareturn( this.text);
    },
    /**
     * put_css: A function that fills the component elements with styles passed from the parent component
     */
    put_css() {
      for (let e of this.css) {
        let k = Object.keys(e);
        let els = document.querySelectorAll('#' + this.id + ' .' + k);
        if (els) {
          for (let css of Object.keys(e[k])) {
            for (let el of els) {
              el.style[css] = e[k][css];
            }
          }
        }
      }

    },
    /**
     * keyEnter: Adjusts the behavior of the component when pressing Enter
     */
    keyEnter() {
      if (this.idx > -1) {
        this.text = this.selectedList[this.idx].name;
        this.idx = -1;
      } else {
        this.selectedList = [];
        this.putValueBack();
      }
    },
    /**
     * keyDown: Moves the cursor down the list of found matches
     */
    keyDown() {
      if (this.selectedList.length > 0) {
        if (this.idx === -1) this.idx = 0; else this.idx++;
      }
    },
    /**
     * keyDown: Moves the cursor up the list of found matches
     */
    keyUp() {
      if (this.selectedList.length > 0 && this.selectedList.length >= this.idx + 1) {
        if (this.idx === 0) this.idx = -1; else this.idx--;
      }
    },
    selectItem(i) {
      this.text = this.selectedList[i].name;
    },
    /**
     * searching: Search for matches with the input string
     */
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
  background-color: #ccc;
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
.ac-button {
  text-align: end;
  padding-right: 10px;
  margin-top: -24px;
  color: #00f;
  height: 24px;
  cursor: pointer;
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
  background-color: #ccc;
  cursor: pointer;
}

.ac-item:nth-last-child(1) {
  border-bottom: none;
  padding-bottom: 6px;
}


</style>