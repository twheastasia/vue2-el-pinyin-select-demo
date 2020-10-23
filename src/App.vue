<template>
  <div id="app">
    <pinyin-select v-model="selected" :options="options" option-value-key="value" option-label-key="label" :filter-keys="['value', 'label']" @change="onSelectChanged" />
    <div>
      绑定值：{{ selected }}
    </div>
    <br>
    <br>
    <pinyin-select-multiple v-model="selecteds" :options="options" option-value-key="value" option-label-key="label" :filter-keys="['value', 'label']" @change="onSelectsChanged" />
    <div>
      绑定值：{{ selecteds }}
    </div>
  </div>
</template>

<script>
import PinyinSelect from './components/PinyinSelect'
import PinyinSelectMultiple from './components/PinyinSelectMultiple'

export default {
  name: 'app',
  components: {
    PinyinSelect,
    PinyinSelectMultiple
  },
  data() {
    return {
      options: [{
        value: '选项1',
        label: '黄金糕'
      }, {
        value: '选项2',
        label: '双皮奶'
      }, {
        value: '选项3',
        label: '蚵仔煎'
      }, {
        value: '选项4',
        label: '龙须面'
      }, {
        value: '选项5',
        label: '北京烤鸭'
      }],
      selected: '',
      selecteds: []
    }
  },
  methods: {
    onSelectChanged() {
      console.log(this.selected)
    },
    onSelectsChanged() {
      console.log(this.selecteds)
    }
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
  margin-top: 60px;
}
</style>
