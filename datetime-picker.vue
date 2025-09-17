<script setup>
import { ref } from 'vue'

// 弹出控制
const showPicker = ref(false)
// 显示框内容
const displayText = ref('')

// 当前时间
const now = new Date()
const currentHour = now.getHours()
const currentMinute = now.getMinutes()

// 判断是否为今天
const isToday = (dateStr) => {
  const d = new Date(dateStr)
  return (
    d.getFullYear() === now.getFullYear() &&
    d.getMonth() === now.getMonth() &&
    d.getDate() === now.getDate()
  )
}

// 生成未来 7 天日期列
const days = Array.from({ length: 7 }, (_, i) => {
  const d = new Date()
  d.setDate(now.getDate() + i)
  return {
    text: `${d.getMonth() + 1}月${d.getDate()}日`,
    value: d.toDateString()
  }
})

// 完整小时/分钟列
const fullHours = Array.from({ length: 24 }, (_, i) => ({ text: `${i}时`, value: i }))
const fullMinutes = Array.from({ length: 60 }, (_, i) => ({ text: `${i}分`, value: i }))

// 初始化小时/分钟列（今天从当前时间开始）
const initialHours = Array.from({ length: 24 - currentHour }, (_, i) => ({
  text: `${currentHour + i}时`,
  value: currentHour + i
}))

const initialMinutes = Array.from({ length: 60 - currentMinute }, (_, i) => ({
  text: `${currentMinute + i}分`,
  value: currentMinute + i
}))

// 响应式列
const columns = ref([days, initialHours, initialMinutes])

// Picker 确认选择
const onConfirm = ({ selectedOptions }) => {
  const textValues = selectedOptions.map(opt => opt.text)
  displayText.value = textValues.join(' ')

  const d = new Date(selectedOptions[0].value)
  d.setHours(selectedOptions[1].value)
  d.setMinutes(selectedOptions[2].value)

  // ISO 北京时间
  const pad = (n) => n.toString().padStart(2, '0')
  const isoValue = `${d.getFullYear()}-${pad(d.getMonth() + 1)}-${pad(d.getDate())}T${pad(d.getHours())}:${pad(d.getMinutes())}:00+08:00`

  console.log('选择文本:', displayText.value)
  console.log('最终 Date (北京时间 ISO):', isoValue)

  showPicker.value = false
}

// Picker 联动事件
const onChange = ({ columnIndex, selectedValues }) => {
  console.log(columnIndex);
  console.log(selectedValues);
  if (columnIndex === 0) { // 日期列变化
    const selectedDate = selectedValues[0]
    if (isToday(selectedDate)) {
      // 今天 → 小时从当前小时开始
      columns.value[1] = Array.from({ length: 24 - currentHour }, (_, i) => ({
        text: `${currentHour + i}时`,
        value: currentHour + i
      }))
      columns.value[2] = Array.from({ length: 60 - currentMinute }, (_, i) => ({
        text: `${currentMinute + i}分`,
        value: currentMinute + i
      }))
    } else {
      // 未来日期 → 小时/分钟完整
      columns.value[1] = fullHours
      columns.value[2] = fullMinutes
    }
  }

  if (columnIndex === 1) { // 小时列变化
    const selectedDate = selectedValues[0]
    const selectedHour = selectedValues[1]
    if (isToday(selectedDate) && selectedHour === currentHour) {
      columns.value[2] = Array.from({ length: 60 - currentMinute }, (_, i) => ({
        text: `${currentMinute + i}分`,
        value: currentMinute + i
      }))
    } else {
      columns.value[2] = fullMinutes
    }
  }
}
</script>
<template>
  <div>
    <van-field
      label="截止时间"
      v-model="displayText"
      readonly
      clickable
      :value="displayText"
      placeholder="请选择截止时间"
      @click="showPicker = true"
    />

    <van-popup v-model:show="showPicker" round position="bottom">
      <van-picker
        title="选择截止时间"
        :columns="columns"
        @confirm="onConfirm"
        @cancel="() => showPicker = false"
        @change="onChange"
      />
    </van-popup>
  </div>
</template>
