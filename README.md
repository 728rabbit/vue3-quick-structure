# vue3-quick-structure
Vue 3 export default {} 的完整模板，包含 所有常用的參數、函式以及註解，方便快速參考


🔑 使用說明

props：父組件傳入資料，支援類型驗證與預設值。

data()：組件內部狀態。

computed：依賴 reactive 或 props 的衍生狀態，性能優化。

watch：監聽資料變化，做副作用。

methods：定義可在模板或內部呼叫的函式。

生命週期 hooks：追蹤組件初始化 → 渲染 → 更新 → 銷毀流程。

components：註冊子組件。

directives：自訂 DOM 指令。

mixins：把多個組件共用的邏輯（data、methods、computed、watch、生命週期等）抽出來，放進 mixin，組件再引入使用。

provide / inject：跨層級傳遞資料。

emits：定義組件可以發出的事件。
