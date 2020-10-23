<template>
  <el-select
    v-model="selected"
    filterable
    clearable
    :size="size"
    remote
    :remote-method="filterByPinyin"
    :loading="selectLoading"
    :placeholder="placeholder"
    :disabled="disabled"
    @visible-change="onFilterChanged"
    @change="valueChanged"
  >
    <el-option
      v-for="item in filteredOption"
      :key="item[optionValueKey] + new Date().getTime()"
      :value="item[optionValueKey]"
      :label="item[optionLabelKey]"
    />
  </el-select>
</template>

<script>
import PinyinMatch from 'pinyin-match'

export default {
  name: 'PinyinSelect',
  model: {
    prop: 'selectedValue',
    event: 'change'
  },
  props: {
    // 绑定值
    selectedValue: {
      type: String,
      default: function() {
        return ''
      }
    },
    // option数据源
    options: {
      type: Array,
      default: function() {
        return []
      }
    },
    // option数据源中value的标识
    optionValueKey: {
      type: String,
      default: function() {
        return ''
      }
    },
    // option数据源中label的标识
    optionLabelKey: {
      type: String,
      default: function() {
        return ''
      }
    },
    size: {
      type: String,
      default: function() {
        return 'mini'
      }
    },
    loading: {
      type: Boolean,
      default: function() {
        return false
      }
    },
    placeholder: {
      type: String,
      default: function() {
        return '请选择'
      }
    },
    // 可以根据设定好的字段来查找
    filterKeys: {
      type: Array,
      default: function() {
        return ['name']
      }
    },
    disabled: {
      type: Boolean,
      default: function() {
        return false
      }
    }
  },
  data() {
    return {
      filteredOption: this.options,
      selected: this.selectedValue,
      selectLoading: this.loading
    }
  },
  watch: {
    selectedValue: {
      handler(newName) {
        this.selected = newName
      },
      immediate: true,
      deep: true
    },
    options: {
      handler(newName) {
        this.filteredOption = newName
      },
      immediate: true,
      deep: true
    },
    loading: {
      handler(newName) {
        this.selectLoading = newName
      },
      immediate: true,
      deep: true
    }
  },
  methods: {
    filterByPinyin(query) {
      this.filteredOption = this.filterValueByKeys(this.options, this.filterKeys, query)
    },
    onFilterChanged() {
      this.filteredOption = this.options
    },
    valueChanged() {
      this.$emit('change', this.selected)
    },
    filterValueByKeys(originArr, keys, query) {
      // 筛选多个key
      let result = []
      if (query !== '') {
        result = originArr.filter(item => {
          let flag = false
          for (let index = 0; index < keys.length; index++) {
            if (item[keys[index]] && query && PinyinMatch.match(item[keys[index]], query)) {
              flag = true
              break
            }
          }
          return flag
        })
      } else {
        result = []
      }
      return result
    }
  }
}
</script>
