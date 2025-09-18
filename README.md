# vant4-datetime-picker
A custom Vue 3 + Vant 4 picker to select **day, hour, and minute** in a single component.  
Official Vant4 only provides separate date-picker and time-picker, so this combines both.  

English | [中文说明](#中文说明)

---

## Core Features
- **Date column**: next 7 days, e.g., "September 19"
  - Today starts from the current hour and minute
  - Future dates show 0-23 hours and 0-59 minutes
- **Hour column**: linked to date column, adjusts automatically
- **Minute column**: linked to date and hour, ensures valid times
- **Responsive linkage**: uses Vue 3 `ref` + `columns.value`, no need for `pickerRef.value.setColumnValues`
- **Output**: selection text (e.g., "September 19 18:30") and Beijing Time ISO (e.g., `2025-09-19T18:30:00+08:00`)
- **User interaction**: click input (`van-field`) → open picker (`van-popup`), supports confirm, cancel, and swipe events
- **Scalable**: adjustable minute steps, more future days, additional columns possible

## Technical Highlights
- Responsive `columns.value` enables dynamic column updates in Vue 3 + Vant 4
- Ensures today starts from current time; future dates complete
- Outputs ISO format in Beijing Time
- Simple, clean structure; drop into `App.vue` and run

## How to Use
1. Copy the code into your project.
2. Import Vant 4 components (e.g. `Field`, `Popup`, `Picker`) in `main.js(or ts)` or your global registration file.
3. Use the component in a page, such as in App.vue or other pages <DateTimePicker/>.

## Extending
- Change the date range: modify the date generation logic
- Add more columns: follow the pattern of date/hour/minute column definitions
- Adjust minute steps or other display formats as needed

---

## 中文说明
[Back to English](#core-features)

这是一个 **Vue 3 + Vant 4 自定义日期时间选择器**，可以在同一个组件中选择 **日、时、分**。  
官方 Vant4 仅提供单独的日期选择器和时间选择器，这个组件将两者结合。

### 核心功能
- **日期列**：未来 7 天，例如“9月19日”  
  - 今天从当前时间的小时和分钟开始  
  - 未来日期显示完整 0-23 小时，0-59 分钟
- **小时列**：与日期联动，自动更新  
- **分钟列**：与日期和小时联动，保证时间合理  
- **响应式联动**：使用 Vue 3 `ref` + `columns.value`，无需依赖 `pickerRef.value.setColumnValues`  
- **输出**：选择文本（例如“9月19日 18:30”）及北京时间 ISO 格式（例如 `2025-09-19T18:30:00+08:00`）  
- **用户交互**：点击输入框（`van-field`）→ 弹出选择器（`van-popup`），支持确认、取消及滑动事件  
- **可扩展性**：可调整分钟步长、增加未来天数、增加更多列  

### 技术亮点
- 响应式 `columns.value` 实现 Vue 3 + Vant 4 多列动态更新  
- 确保今天从当前时间开始，未来日期完整显示  
- 输出北京时间 ISO 格式  
- 结构简洁，可直接放入 `App.vue` 使用  

### 使用方法
1. 将代码复制到你的项目中.  
2. 在 `main.js(或ts)` 或全局注册文件中导入 Vant 4 组件（如 `Field`、`Popup`、`Picker`）.  
3. 在页面中使用该组件，例如在 App.vue 或其他页面中 <DateTimePicker />.  

### 扩展
- 修改日期范围：调整代码中日期生成逻辑  
- 增加更多列：参考日期/小时/分钟列的生成模式  
- 调整分钟步长或其他显示格式  
