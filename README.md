# vant4-datetime-picker
A custom Vue 3 + Vant 4 picker to select **day, hour, and minute** in a single component. 
Official Vant4 only provides separate date-picker and time-picker, so this combines both.

# Core Features
- **Date column**: next 7 days, e.g., "September 19"
  - Today starts from the current hour and minute
  - Future dates show 0~23 hours and 0~59 minutes
- **Hour column**: linked to date column, adjusts automatically
- **Minute column**: linked to date and hour, ensures valid times
- **Responsive linkage**: uses Vue 3 `ref` + `columns.value`, no need for `pickerRef.value.setColumnValues`
- **Output**: selection text (e.g., "September 19 18:30") and Beijing Time ISO (e.g., `2025-09-19T18:30:00+08:00`)
- **User interaction**: click input (`van-field`) → open picker (`van-popup`), supports confirm, cancel, and swipe events
- **Scalable**: adjustable minute steps, more future days, additional columns possible

# Technical Highlights
- Responsive `columns.value` enables dynamic column updates in Vue 3 + Vant 4
- Ensures today starts from current time; future dates complete
- Outputs ISO format in Beijing Time
- Simple, clean structure; drop into `App.vue` and run


# How to Use
1. Copy the code into your project.
2. Import Vant 4 components (e.g., `Field`, `Popup`, `Picker`) in `main.ts` or your global registration file.
3. Use `<App />` or the component in your page.

# Extending
- Change the date range: modify the date generation logic
- Add more columns: follow the pattern of date/hour/minute column definitions
- Adjust minute steps or other display formats as needed
