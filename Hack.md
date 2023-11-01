my-vue-document
===
View the content with "<i class="fa fa-book fa-fw"></i> vue.js".

>### What is Vue.js?
>是一個漸進式的前端架構

>### Vue 特性
>- Data&Methods 集中管理
>- 與html的結合
>- component的組成

在 Vue.js 中，組件通常由三個主要部分組成
- `<template>`
- `<script>`
- `<style>`

這些部分共同定義了組件的外觀、行為和樣式。

- `<template>` 部分包含了組件的 HTML 結構，用於定義組件的外觀和佈局。在模板中，您可以使用 Vue 的模板語法，包括插值、指令、事件處理程序等，來描述組件的呈現方式。模板部分是組件的視圖，它決定了組件在頁面上的顯示效果。

- `<script>` 部分包含了組件的 JavaScript 邏輯。您可以在這裡定義組件的數據、計算屬性、方法和生命週期鉤子等。這是組件的行為邏輯部分，用於處理數據和響應用戶交互。

- `<style>` 部分包含了組件的 CSS 樣式。您可以在這裡定義組件的樣式規則，以確保組件的外觀滿足設計要求。Vue 支持多種樣式語法，包括普通的 CSS、預處理器（如 SASS 和 LESS）以及 CSS 框架（如 Bootstrap）。

組件的 `<template>`、`<script>` 和 `<style>` 部分通常一起工作，協同構建完整的組件。這種組織方式使得組件的結構清晰，易於維護和重用，同時提供了一種聲明性的方式來描述頁面的佈局和交互邏輯。

# Overview

- ### Essentials

- ### Components In-Depth


## Essentials

### 1.創建一個Vue應用
- 使用el綁定ID
`el` 屬性是Vue.js中的一個選項，它用於指定Vue實例應該掛載到哪個DOM元素上。它的名稱是"element"的縮寫。當你在Vue實例中設置 `el` 屬性時，Vue將會將應用程序掛載到指定的DOM元素上，並開始管理該元素及其內容。
   - 直接使用 el:“#app” 掛載
   - 在需要時再使用 $mount(“#app”) 掛載的功能
- Vue的應用程式不能巢狀排列，巢狀排列指可以是將循環或條件語句放在另一個內部，以處理複雜的邏輯或數據結構。

>使用`el`屬性直接掛載：
```vue=
<div id='app'>
   //  這是將安裝Vue.js應用程式的容器
   {{ text }}
</div>

<script>
// 創建一個新的Vue實例並將其指定給變數'app'
var app = new Vue({
   // 'el'指定Vue將要掛載的HTML元素
   el: '#app',
   
   // 'data'是一個物件，定義了Vue實例的初始資料
   data: {
      // 'text'屬性被定義為初始值為'hello'
      text: 'hello'  // 在這裡設定data的初始值
   }
})
</script>
```

>使用`$mount`方法：
```vue=
<script>
// 建立一個新的 Vue 實例
var app = new Vue({
   data: {
      text: '你好'  // 在這裡設定 data 的初始值
   }
})

// 手動將 Vue 實例掛載到指定的元素上
app.$mount('#app');
</script>
```




### 2.模板語法
- 插值: 使用 `{{ }}` 將數據嵌入模板，實現數據渲染，把vue中的變數呈現在前端。

- 指令: 以 `v-` 開頭的特殊屬性，實現數據綁定和操作DOM。
   - `v-bind`: 綁定元素屬性，例如 `v-bind:href="url"` 會將元素的`href`屬性綁定到`url`變數。
   - `v-on`: 監聽事件，如 `v-on:click="doSomething"` 會在點擊事件發生時執行`doSomething`函數。
   - `v-if`, `v-else-if`, `v-else`: 條件渲染。
   - `v-for`: 列表渲染。
   - `v-model`: 雙向數據綁定，透過`{{ }}`綁定文字，基本上 v-model 只會用在 input, textarea, select 這些傳入資訊的元素。

- 過濾器: 用於格式化數據，例如，`{{ message | capitalize }}` 可以將 `message` 的值轉為首字母大寫。

- 事件處理: 使用 `v-on` 監聽DOM元素上的事件，執行相關JavaScript代碼。

- 雙向數據綁定: 使用 `v-model` 實現表單元素值與數據的雙向關聯。

- 計算屬性: 使用 `computed` 定義根據數據計算的派生屬性。這些屬性會基於資料的變化而自動更新，而不需要手動更新。

>試著將 class 綁定加到這個 h1 上，並使用 titleClass 的 ref 作為它的值。如果綁定正確，文字將會變成綠色。
```vue=
<script setup>
//引入 ref 函數並創建名為 titleClass 的 ref 變數，初始值為 'title'
//代表將一個響應式的字符串 'title' 儲存在 titleClass 變數中。
import { ref } from 'vue'
const titleClass = ref('title')
</script>

<template>
  //使用 :class 綁定將 titleClass 變數作為 CSS 類別綁定到 <h1> 標籤，從而使標題文本變成綠色。
  <h1 :class="titleClass">變綠</h1>
</template>

<style>
// 在樣式中定義 .title 類別，設定文本顏色為綠色 
.title {
  color: green;
}
</style>
```
這段程式碼演示了如何使用Vue的`ref`和`:class`指令來動態地改變HTML元素的CSS類別，進而改變它的樣式。


### 3.響應式基礎

響應式是Vue.js的基礎，使開發者能夠輕鬆構建動態的Web應用程序。
- Vue.js的核心特點是響應式（Reactivity）。
- 數據模型的變化會自動反映在UI（用戶介面）上。
- Vue實例的data屬性包含響應式數據。
- 模板中使用插值和指令來展示響應式數據。
- 可以使用計算屬性和監聽器自訂響應邏輯。
- Vue也處理數組的響應性。
- 嵌套數據和有限制的響應性。

要創建響應式狀態，可以使用`reactive()`或`ref()`。
> 使用ref()
```vue=
<script setup>
// 引入 Vue 3 Composition API 中的 ref 函数
import { ref } from 'vue'

// 創建一個 ref 變數 count，並初始化為 0
const count = ref(0)

// 創建一個名為 increment 的函數，用於增加 count 的值
function increment() {
  count.value-- // 減少 count 的值
}
</script>

<template>
  // 點擊按鈕時調用 increment 函數，並顯示 count 的值 
  <button @click="increment">
    {{ count }}
  </button>
</template>
```
> 使用reactive()
```vue=
<script setup>
// 引入 Vue 3 Composition API 中的 reactive 
import { reactive } from 'vue'

// 創建一個 reactive 物件，包含 count 屬性並初始化為 0
const counter = reactive({ count: 0 })

// 創建一個名為 increment 的函數，用於增加 count 的值
function increment() {
  state.count-- // 減少 count 的值
}
</script>

<template>
  // 點擊按鈕時調用 increment 函數，並顯示 count 的值 
  <button @click="increment">
    {{ state.count }}
  </button>
</template>
```
總之，`reactive()` 用於創建包含多個響應式屬性的物件，而 `ref()` 用於包裝單個值，使其成為響應式。您可以根據具體的需求和數據結構選擇使用哪種方式。

>結合`reactive()`和`ref()`
```vue=
<script setup>
import { reactive, ref } from 'vue'

// 使用reactive()建立一個名為counter的響應式對象
const counter = reactive({ count: 0 })

// 使用ref()建立一個名為message的ref
const message = ref('I am Amber!')
</script>

<template>
  <h1>{{ message }}</h1>
  <p>Count is: {{ counter.count }}</p>
</template>
```

### 4.計算屬性
- 計算屬性是用於處理複雜邏輯的工具。
- 使用 `computed` 函數來創建計算屬性。
- 計算屬性具有緩存功能，提高性能。
- 可以創建可寫的計算屬性。
- 最佳實踐包括確保計算屬性的 getter 保持乾淨，避免直接修改計算屬性的值。
- 屬於派生屬性：
   - 依賴於其他屬性：派生屬性的值取決於一個或多個其他屬性的值。當這些依賴屬性的值發生變化時，派生屬性的值通常會自動更新。

   - 不存儲獨立的數據：派生屬性通常不會存儲獨立的數據，而是通過計算得出。這有助於確保數據的一致性，因為它們不需要手動更新。

   -  提供有用信息或輔助計算：派生屬性通常用於提供便於操作和理解的信息，或者用於執行進一步的計算。它們可以用於數據轉換、格式化、篩選等操作。
```vue=
<script setup>
import { ref } from 'vue'

let id = 0

// 創建一個名為 newTodo 的 ref 變數，用於存儲新待辦事項的文本
const newTodo = ref('')

// 創建一個名為 hideCompleted 的 ref 變數，用於控制是否隱藏已完成的待辦事項
const hideCompleted = ref(false)

// 創建一個名為 todos 的 ref 變數，用於存儲待辦事項的清單
const todos = ref([
  { id: id++, text: '電子化企業', done: true },
  { id: id++, text: '資料探勘', done: true },
  { id: id++, text: '行為資料分析', done: false }
])

// 定義一個名為 addTodo 的函數，用於添加新的待辦事項
function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

// 定義一個名為 removeTodo 的函數，用於刪除待辦事項
function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
  // 輸入框綁定到 newTodo 變數 
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
    // 複選框綁定到 todo.done，用於標記已完成的待辦事項 
      <input type="checkbox" v-model="todo.done">
       //  待辦事項的文字內容，如果已完成，則新增樣式 done
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      //  按鈕用於刪除待辦事項，並綁定到 removeTodo 函數 
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  //  按鈕用於切換是否隱藏已完成的待辦事項 
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
  // 已完成的待辦事項使用刪除線樣式
}
</style>
```

### 5.類別樣式綁定
當需要在Vue.js中控制HTML元素的類別和內聯樣式時，你可以使用`v-bind:class`和`v-bind:style`指令來綁定HTML元素的class（類名）和inline style（內聯樣式）。

-  **類別綁定**：
   - **物件語法**：你可以使用物件來定義哪些類名應該添加到HTML元素上。物件的鍵是類名，而值是一個布林值，表示該類是否應添加。例如：
   
     ```html
     <div v-bind:class="{ active: isActive }"></div>
     ```
   
     在這個例子中，如果 `isActive` 為真，那麼元素將擁有 `active` 這個類名。

   - **陣列語法**：你也可以使用陣列，將多個類名以陣列方式添加到元素上。例如：
   
     ```html
     <div v-bind:class="[activeClass, errorClass]"></div>
     ```
   
     在這個例子中，`activeClass` 和 `errorClass` 是你事先定義的變數，包含類名，這些類名都會應用到元素上。

-  **內聯樣式綁定**：

   - **物件語法**：你可以使用物件定義CSS屬性和對應的樣式值，以設定元素的內聯樣式。例如：

     ```html
     <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
     ```

     在這個例子中，`activeColor` 和 `fontSize` 是變數，它們將決定元素的文本顏色和字體大小。

   - **陣列語法**：使用陣列可以同時套用多個樣式物件。這是有用的，特別是當你需要組合多個樣式物件時。例如：

     ```html
     <div v-bind:style="[baseStyles, overridingStyles]"></div>
     ```

     在這個例子中，`baseStyles` 和 `overridingStyles` 都是物件，它們的樣式將合併應用到元素上。

### 6.條件渲染
這段教程介紹了在Vue.js中進行條件渲染的方法：
>v-if & v-else-if v-else 必須連用
>v-model 為取得input的值
- `v-if`：用於根據表達式的真值條件來渲染內容。內容只在表達式為真時才會渲染。
- `v-else`：用於在`v-if`的條件下添加一個“else區塊”來渲染不同的內容。
- `v-else-if`：用於添加“else if區塊”，可以多次使用。
- `<template>`上的`v-if`：`v-if`可以在一個不可見的`<template>`元素上使用，作為包裝器，最終渲染的結果不包含`<template>`元素。
- `v-show`：另一種根據條件來顯示元素的指令，與`v-if`不同，它僅切換CSS屬性而不銷毀和重建元素。
- `v-if` vs. `v-show`：`v-if`是“真實的”條件渲染，會銷毀和重建元素，而`v-show`僅切換CSS display屬性。
- `v-if`和`v-for`：不建議同時使用，`v-if`的優先級高於`v-for`，風格指南中有更多信息。

1. **`v-if` 和 `v-else`**：這兩個指令讓你可以根據表達式的真偽來渲染不同的內容。在這個示例中，我們有一個變數 `awesome`，它的值初始為真（`true`）。當你點擊按鈕時，`awesome` 的值會切換成假（`false`）。根據這個 `awesome` 的值，我們使用 `v-if` 和 `v-else` 來渲染不同的標題。

   - 如果 `awesome` 為真，則渲染 "My name is Amber!"。
   - 否則，如果 `awesome` 為假，則渲染 "Hello"。

2. **`<template>` 上的 `v-if`**：你可以將 `v-if` 放在不可見的 `<template>` 元素上，作為包裝器，最終渲染的結果不包含 `<template>` 元素。這在組織複雜的條件渲染內容時很有用。

3. **`v-show`**：這個指令與 `v-if` 不同。它用於根據條件切換元素的可見性，但不會銷毀和重建元素，只是切換CSS的`display`屬性。如果你需要頻繁地切換元素的可見性而不想引起重建的開銷，則可以使用 `v-show`。

4. **`v-if` vs. `v-show`**：`v-if`是“真實的”條件渲染，當條件為假時，元素會被銷毀，當條件為真時，元素會重新創建。相對地，`v-show`僅切換CSS的`display`屬性，不會銷毀和重建元素。你可以根據情況選擇使用哪個。

5. **`v-if` 和 `v-for`**：在同一個元素上不建議同時使用這兩個指令，因為 `v-if` 的優先級高於 `v-for`。代表如果你在一個元素上同時使用它們，`v-if` 的條件將優先適用，可能會影響你的渲染結果。

這些指令可以在模板中渲染或切換內容，實現了動態渲染的效果。

>試著為範例新增 v-if 和 v-else 指令，並實作 toggle() 方法，讓我們可以使用按鈕在它們之間切換。
```vue=
<script setup>
import { ref } from 'vue'

// 創建一個名為 awesome 的 ref 變數，初始值為 true
const awesome = ref(true)

// 定義一個名為 toggle 的函數，用於切換 awesome 變數的值
function toggle() {
  awesome.value = !awesome.value
}
</script>

<template>
  //按鈕，當點擊時調用 toggle 函數 
  <button @click="toggle">toggle</button>
  
  <//標題，根據 awesome 變數的值動態顯示不同的內容
  <h1 v-if="awesome">I am Amber</h1>
  <h1 v-else>Hello</h1>
</template>
```

### 7.列表渲染

- **v-for 指令**：是 Vue.js 中用來渲染清單的重要工具。語法是 item in items，其中 items 是資料數組，item 是用於迭代的別名。
- **存取父作用域**：在 v-for 區塊內，可以存取父作用域的屬性和變數。這表示可以在清單項目內使用父作用域的資料。
- **位置索引**：v-for 也支援使用可選的第二個參數表示目前項目的位置索引。例如：(item, index) in items，這允許您存取目前項目在陣列中的位置。
- **作用域與 forEach 類似**：v-for 變數的作用域類似於 JavaScript 的 forEach 回呼函數，可以在其中存取目前項目的屬性和父作用域的資料。
- **解構**：您可以在 v-for 的別名中使用解構，例如 { message } 或 { message, index }，以快速存取物件的屬性。
- **多層嵌套**：每個 v-for 區塊都可以存取其父級作用域，這允許您在嵌套清單中存取不同層級的資料。
- **遍歷物件屬性**：除了數組，v-for 也可以用於遍歷物件的所有屬性。物件屬性的遍歷順序是基於呼叫 Object.keys() 的傳回值，通常是屬性的插入順序。
- **key 屬性**：在 v-for 中，建議為每個渲染的元素提供一個唯一的 key 屬性。這有助於 Vue 識別和重複使用元素，提高效能。
- **v-if 和 v-for 的優先權**：當 v-if 和 v-for 同時使用時，v-if 的優先權高於 v-for。且不建議 v-for 與 v-if 一起使用時，如有這種狀況建議使用 computed 屬性，讓其回傳過濾後的列表。
- **響應式陣列的變更監聽**：Vue 能夠監聽響應式陣列的變更方法，包括 push、pop、shift、unshift、splice、sort 和 reverse。這表示如果您使用這些方法修改數組，視圖將自動更新以反映這些變更。

>嘗試實現`addTodo()`和`removeTodo()`方法，以使列表能夠正常工作，允許添加和刪除待辦事項。這是Vue中列表渲染的基本示例。
```vue=
<script setup>
import { ref } from 'vue'

// 給每個 todo 物件一個唯一的 id
let id = 0

// 創建一個名為 newTodo 的 ref 變數，用於存儲新待辦事項的文本
const newTodo = ref('')

// 創建一個名為 todos 的 ref 變數，用於存儲待辦事項的清單
const todos = ref([
  { id: id++, text: '電子化企業' },
  { id: id++, text: '資料探勘' },
  { id: id++, text: '行為資料分析' }
])

// 定義一個名為 addTodo 的函數，用於添加新的待辦事項
function addTodo() {
// 新增待辦事項到 todos 列表
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = '' // 清空輸入框
}

// 定義一個名為 removeTodo 的函數，用於刪除待辦事項
function removeTodo(todo) {
// 使用 filter 方法過濾待辦事項列表，刪除指定的待辦事項
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
  // 使用 v-model 將 <input> 中的值與 newTodo 變數雙向綁定
    <input v-model="newTodo">
    <button>Add Todo</button>    
  </form>
  <ul>
  // 使用 v-for 遍歷 todos 清單中的待辦事項，並使用 :key 來指定每個待辦事項的唯一標識
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }} // 顯示待辦事項的文字 
      <button 
      //  按鈕，點擊時呼叫 removeTodo 函數刪除該待辦事項 
      @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>
```
- 動態產生多筆資料於畫面上
- 當括號中有不同筆數的資料，變數也代表不同意思
  - v-for="(itemValue,item,index) in array"
  - v-for="(item,index) in array"
  - v-for="item in array"
itemValue : 回傳的是陣列中的屬性值。冒號:後
item : 回傳的是陣列中的屬性名稱。冒號:前
index : 回傳的是陣列中的索引值
### 8.事件處理
事件處理是關鍵的交互式技術之一。
=
- **內聯事件處理器**：
   - 在模板中，你可以使用 `@事件名` 或 `v-on:事件名` 來設定內聯事件處理器。

    使用 `v-on` 指令來監聽 DOM 事件： 
    ```vue
    <button v-on:click="increment">{{ count }}></button>
    ```

    `v-on` 也有簡寫語法：
    ```vue
    <button @click="increment">{{ count }}</button>
    ```
   - 事件處理器直接內嵌在模板中，通常在元素的事件屬性上定義。
   ```vue
   <template>
  <button @click="increment">增加</button>
   </template>
    ```

   - 內聯事件處理器通常是簡單的函數或表達式，例如 `@click="doSomething"`，其中 `doSomething` 是在組件中定義的方法或表達式。
   - 內聯事件處理器可以存取組件中的數據，但通常只能進行簡單的操作。
#### 內聯事件處理器
```vue=
<script setup>
// 引入 Vue 3 的 ref 函數
import { ref } from 'vue'

// 創建一個名為 counter 的 ref 屬性，並初始化為 0
const counter = ref(0)
</script>

<template>
	// 按鈕元素，當點擊時執行 counter++ 
	<button @click="counter++">Add 1</button>

	// 顯示計數的段落元素 
	<p>The button above has been clicked {{ counter }} times.</p>
</template>
```
- **方法事件處理器**：
   - 在Vue.js組件中，你可以在 `methods` 區塊中定義方法，然後在模板中使用內聯事件處理器來調用這些方法。
   - 方法事件處理器通常用於處理複雜的邏輯或需要重複使用的代碼。
   - 使用方法事件處理器使代碼更結構化和可讀，因為你可以將相關的事件處理邏輯組織在一個或多個方法中。
   - 方法事件處理器可以接受參數，這些參數可以根據事件的上下文進行操作。
#### 方法事件處理器
```vue==
<script setup>
import { ref } from 'vue'

const name = ref('I am Amber')

// 定義一個名為 `greet` 的方法，該方法會顯示警示框
// 以及事件目標的標籤名（如果有事件參數）
function greet(event) {
  // 顯示一個包含問候信息的警示框，使用模板字符串引用 `name.value`
  alert(`Hello ${name.value}!`)
  // `event` 是原生 DOM 事件對象
  if (event) {
    // 如果存在 `event`，則顯示被點擊元素的標籤名稱
    alert(event.target.tagName)
  }
}
</script>

<template>
  // 在按鈕上添加點擊事件，當按鈕被點擊時調用 `greet` 方法 
  <button @click="greet">clickme</button>
</template>
```
簡而言之，內聯事件處理器是直接在模板中定義的事件處理函數，而方法事件處理器是在 `methods` 區塊中定義的方法，用於處理事件，使代碼更組織化且易於維護。通常建議在方法事件處理器中處理較複雜的邏輯，而在內聯事件處理器中處理簡單的任務。

### 9.表單輸入設定
在Vue.js中，`v-model`指令是處理表單輸入的重要工具，允許輕鬆實現雙向數據綁定和事件監聽。

- **基本用法**：`v-model`可以用於文本輸入框，實現輸入框的值和Vue組件數據的雙向綁定。這意味著當輸入框的值變化時，關聯的數據也會自動更新。

- **多行文本**：對於多行文本輸入框（`<textarea>`），同樣可以使用`v-model`來雙向綁定文本內容。

- **複選框**：`v-model`可用於綁定布爾類型的數據，使其與複選框的選中狀態同步。這使得在表單中處理多個複選框非常方便。

- **多個複選框**：你可以將多個複選框綁定到同一個數組，以跟蹤多個選項的選擇狀態。選中的選項的值將添加到數組中。

- **單選按鈕**：單選按鈕也可以使用`v-model`綁定到一個變數，以跟蹤當前選中的單選按鈕的值。

- **選擇器**：`v-model`可用於綁定選擇器（`<select>`）的選中項。你可以使用`<option>`元素來定義可選項。

- **修飾符**：Vue提供了修飾符，如`.lazy`、`.number`和`.trim`，以自定義`v-model`的行為。這些修飾符可以控制數據何時更新以及如何處理輸入。

- **自定義組件**：`v-model`也可以在自定義Vue組件中使用，允許你實現自定義的表單輸入行為並支持雙向綁定。

總之，`v-model`是Vue.js中一個非常強大和便捷的工具，用於簡化前端表單處理和數據綁定的操作，有助於構建交互性強大的Vue.js應用程序。 

#### 文本
```javascript=
<script setup>
import { ref } from 'vue'

// 創建一個名為 `message` 的 ref 變數，用於存儲輸入框的值
const message = ref('')
</script>

<template>
  <p>Message is: {{ message }}</p>
  //使用 v-model 指令將輸入框的值綁定到 `message` 變數 
  <input v-model="message" placeholder="edit me" />
</template>
```
#### 多行文本
```javascript=
<script setup>
// 引入 Vue 3 的 ref 函數
import { ref } from 'vue'

// 創建一個名為 message 的 ref 屬性，並初始化為空字串
const message = ref('')
</script>

<template>
	// 顯示多行消息的標題 
	<span>Multiline message is:</span>
	
	// 顯示消息內容，並使用 "white-space: pre-line" 样式来支持多行文本 
	<p style="white-space: pre-line;">{{ message }}</p>
	
	// 用 textarea 元素來輸入多行消息，使用 v-model 雙向綁定 message 屬性 
	<textarea v-model="message" placeholder="add multiple lines"></textarea>
</template>
```

#### 複選框
```javascript=
<script setup>
// 引入 Vue 3 的 ref 函數
import { ref } from 'vue'

// 創建一個名為 checkedNames 的 ref 屬性，並初始化為一個空數組，用於存儲已選中的名字
const checkedNames = ref([])
</script>

<template>
  // 顯示已選中的名字 
  <div>Checked names: {{ checkedNames }}</div>

  //三個選擇框，每個選擇框都與 checkedNames 進行雙向綁定 
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
  <label for="jack">Jack</label>

  <input type="checkbox" id="john" value="John" v-model="checkedNames" />
  <label for="john">John</label>

  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
  <label for="mike">Mike</label>
</template>
```
#### 單選按鈕
```javascript=
<script setup>
// 引入 Vue 3 的 ref 函數
import { ref } from 'vue'

// 創建一個名為 picked 的 ref 屬性，並初始化為 'One'，用於存儲已選中的選項
const picked = ref('One')
</script>

<template>
  // 顯示已選中的選項 
  <div>Picked: {{ picked }}</div>

  // 兩個單選按鈕，每個單選按鈕與 picked 進行雙向綁定 
	<input type="radio" id="one" value="One" v-model="picked" />
	<label for="one">One</label>

	<input type="radio" id="two" value="Two" v-model="picked" />
  <label for="two">Two</label>
</template>
```
#### 選擇器
```javascript=
<script setup>
// 引入 Vue 3 的 ref 函数
import { ref } from 'vue'

// 创建一个名为 selected 的 ref 属性，并初始化为空字符串
const selected = ref('')
</script>

<template>
  // 显示已选择的选项 
  <span> Selected: {{ selected }}</span>

   // 下拉框元素，使用 v-model 进行双向绑定 
  <select v-model="selected">
    // 禁用的选项，值为空字符串，用于占位提示 
    <option disabled value="">Please select one</option>
    // 可选的选项 
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
</template>

```
### 10.生命週期
- Vue 組件生命週期允許您在組件的創建、更新和銷毀階段執行自定義代碼。

- 常用的生命週期鈎子函數包括 `created`、`mounted`、`updated`、`beforeUnmount` 和 `unmounted`。

- 在 Vue 3 中，使用 Composition API 的 `onMounted`、`onUpdated` 和 `onUnmounted` 來註冊生命週期鈎子函數。
  - `onMounted`：在組件完成初始渲染並掛載到 DOM 後執行，通常用於訪問 DOM 元素。

  - `onUpdated`：在組件數據更新後執行，用於處理數據變化後的操作。

  - `onUnmounted`：在組件銷毀（從 DOM 中卸載）後執行，通常用於清理和取消監聽器等操作。

- 生命週期鈎子函數應在組件初始化時同步註冊，避免在其中進行異步操作。

- 自定義操作，如數據初始化、DOM 操作、清理工作，可以在不同生命週期階段執行。

- 學習 Vue 組件生命週期是提高 Vue.js 應用程序質量、性能和可維護性的關鍵。


### 11.偵聽器
在Vue 3的組合式API中，你可以使用`watch`和`watchEffect`來實現偵聽器響應式狀態的變化並執行相關回調函數。偵聽器的目的是執行「互動」操作，例如修改DOM或根據非同步操作的結果修改狀態。
```javascript=
<script setup>
import { ref, watch } from 'vue'

const question = ref('')
const answer = ref('Questions usually contain a question mark. ;-)')

// 監聽問題的變化
watch(question, async (newQuestion) => {
  if (newQuestion.indexOf('?') > -1) {
    answer.value = 'Thinking...'
    try {
      // 進行API請求以獲取答案
      const res = await fetch('https://yesno.wtf/api')
      answer.value = (await res.json()).answer
    } catch (error) {
      answer.value = 'Error! Could not reach the API. ' + error
    }
  }
})
</script>

<template>
  <p>
    Ask a yes/no question:
    // 使用v-model實現問題和input元素之間的雙向綁定
    <input v-model="question" />
  </p>
  <p>{{ answer }}</p>
</template>
```

### 12.模板引用
在Vue 3中，你可以使用`ref`和模板中的`ref`属性來獲取對DOM元素或子組件的引用，以便訪問和操作它們。

- 獲取DOM元素的引用：
   - 通過在模板中的DOM元素添加`ref`屬性，然後在`<script setup>`中創建一個同名的`ref`來存儲對該DOM元素的引用。
   - 可以在組件掛載後訪問和操作這個DOM元素，例如設置焦點。

- 訪問模板引用：
   - 通過在`<script setup>`中聲明一個同名的`ref`，你可以在組件掛載後通過`ref.value`來訪問DOM元素。
   - 應該確保在訪問之前檢查`ref.value`是否為null以防止訪問未掛載的元素。

- 使用模板引用的函數：
   - 你還可以將`ref`屬性設置為一個函數，該函數在每次組件更新時都會被調用，並接收元素引用作為參數。
   - 這對於需要在每次更新時執行操作的情況很有用。

- 子組件上的模板引用：
   - 你可以在父組件中使用模板引用來訪問和操作子組件的實例。
   - 這允許在父組件中直接與子組件進行通信，並操作子組件的屬性和方法。

>注意事項：
>- 模板引用應該謹慎使用，因為它們可能引入複雜的耦合。通常應優先使用標準的props和emit接口來實現父子組件之間的交互。
>- 在訪問模板引用之前，應確保元素已經掛載到DOM上，以避免訪問未掛載的元素。

```javascript=
<script setup>
import { ref, onMounted } from 'vue'

const list = ref([1, 2, 3])

// 創建一個ref來存儲li元素的引用
const itemRefs = ref([])

onMounted(() => {
  // 在組件被掛載後，顯示所有li元素的內容
  alert(itemRefs.value.map(i => i.textContent))
})
</script>

<template>
  <ul>
    // 使用v-for迭代list中的項目，同時將每個li元素的引用存儲在itemRefs中 // 
    <li v-for="item in list" ref="itemRefs">
      {{ item }}
    </li>
  </ul>
</template>
```


### 13.組件基礎
- 使用 `ref` 屬性為 DOM 元素添加引用，然後在 `<script setup>` 中創建相應的 `ref`，以在組件掛載後訪問和操作 DOM 元素。

- 通過在 `<script setup>` 中聲明同名的 `ref`，可以在組件掛載後通過 `ref.value` 訪問 DOM 元素。請確保在訪問前檢查 `ref.value` 是否為 null。

- 可以將 `ref` 屬性設置為一個函數，該函數在組件更新時將被調用，並接收元素引用作為參數，這對需要執行操作的情況非常有用。

- 在子組件上使用模板引用，引用中的值將是子組件的實例。通常，應優先使用 props 和 emit 來實現父子組件之間的交互，避免濫用模板引用。



## Components In-Depth

### 1.組件註冊
- **全局註冊**：全局註冊是透過應用實例的 `app.component()` 方法實現的，使組件在整個 Vue 應用中可用。你需要為組件定義一個名稱，然後將其實現傳遞給 `app.component()` 方法。全局註冊的組件可以在應用的任何地方使用，包括其他組件的模板中。

- **局部註冊**：局部註冊的組件只能在其父組件中使用，適用於單個組件和較小的項目。在使用 `<script setup>` 的單文件組件中，你可以直接導入並使用組件，無需顯式註冊。如果沒有使用 `<script setup>`，你需要使用 `components` 選項來顯式註冊。

- **組件名稱格式**：在 Vue 中，通常使用 PascalCase 格式來註冊組件名稱。這是因為 PascalCase 是合法的 JavaScript 標識符，也使模板中的組件更容易識別。Vue 也支持使用 kebab-case 的標籤名，它會被解析為 PascalCase 格式的組件名。因此，你可以使用 `<MyComponent>` 或 `<my-component>` 來引用同一個組件。


### 2.props
- **Props聲明**：組件需要顯式聲明它所接受的 props，這樣 Vue 才能知道外部傳入的哪些是 props。在 `<script setup>` 中，你可以使用 `defineProps()` 宏來聲明 props。在普通組件中，你可以使用 `props` 選項。

- **Props傳遞**：Props可以通過靜態值或動態綁定傳遞給組件。你可以使用 `v-bind` 或 `:` 來進行動態綁定。

- **傳遞不同類型的值**：Props可以接收不同類型的數據，如數字、字符串、布爾、數組和對象。你可以自定義類型校驗，並在傳遞錯誤類型時產生警告。

- **單向數據流**：Props遵循單向數據流的原則，子組件不能修改它們。任何修改 props 的嘗試會導致Vue發出警告。

- **Props的校驗**：你可以聲明對傳入的 props 的校驗要求，包括類型、是否必須、默認值等。這對於組件的文檔和安全性很有幫助。

- **運行時類型檢查**：Vue 會在運行時根據 prop 的類型標註進行編譯，並在檢查失敗時發出控制台警告。

- **布爾類型轉換**：對於聲明為布爾類型的 props，存在特殊的類型轉換規則，允許更自然的用法，例如傳遞 `true` 或 `false`，或者使用布爾屬性。

### 3.組件事件

- **觸發事件**：在組件內部，你可以使用 `$emit` 方法來觸發自定義事件，例如：`$emit('someEvent')`。通常，這是在組件的模板表達式中使用，例如在一個點擊事件處理函數內。

- **監聽事件**：父組件可以使用 `v-on` 或 `@` 來監聽事件，例如：`<MyComponent @some-event="callback" />`。事件名稱大小寫會自動轉換，推薦使用 kebab-case 形式。

- **事件參數**：你可以在觸發事件時傳遞額外的參數。這可以通過在 `$emit` 中提供參數，然後在父組件中的監聽器函數中接收它們。

- **聲明觸發的事件**：組件可以顯式聲明要觸發的事件，以便在組件的文檔中記錄事件的用法。這可以通過 `defineEmits()` 宏或 `emits` 選項（在 setup 中使用）來完成。

- **事件校驗**：你可以為觸發的事件添加校驗，以確保事件的合法性。這可以通過在 `defineEmits()` 中或 `emits` 選項中定義一個函數來實現。


### 4.組件v-model
- **在組件上使用 v-model**：`v-model` 可以在自定義組件上使用，以實現雙向綁定。當在組件上使用時，它會被展開為包含 `modelValue` prop 和 `update:modelValue` 事件的方式，用於與組件內部進行數據的雙向綁定。

- **組件內部的實現**：在組件內部，你需要將內部原生 `<input>` 元素的 `value` 屬性綁定到 `modelValue` prop，並在原生 `input` 事件觸發時觸發一個帶有新值的 `update:modelValue` 自定義事件。

- **自定義參數**：你可以為 `v-model` 指定一個參數，以更改默認的 prop 名和事件名。例如，`<MyComponent v-model:title="bookTitle" />` 中的參數是 `title`，所以子組件需要聲明 `title` prop 並使用 `update:title` 事件。

- **處理多個 `v-model`**：你可以在單個組件上創建多個 `v-model` 雙向綁定，每個 `v-model` 同步不同的 prop。只需聲明相應的 `modelValue` prop 和 `update:modelValue` 事件即可。

- **處理 `v-model` 修飾符**：你可以為自定義組件的 `v-model` 添加自定義修飾符，通過 modelModifiers prop 在組件內訪問修飾符。這可以用於自定義處理輸入數據，例如將輸入的字符串首字母大寫等。

- **帶參數的 `v-model` 修飾符**：對於具有參數和修飾符的 `v-model` 綁定，生成的 prop 名將是 `arg + "Modifiers"`，例如 `v-model:title.capitalize="myText"` 中的 `titleModifiers`。


### 5.透傳 Attributes 
- **Attributes 繼承**：透傳 attribute 是指傳遞給組件但沒有在組件內聲明為 props 或 emits 的 attribute 或 v-on 事件監聽器。常見的透傳屬性包括 `class`、`style` 和 `id`。當組件只有一個根元素時，透傳的 attribute 會自動添加到根元素上。

- **對 class 和 style 的合併**：透傳的 `class` 和 `style` 會與組件內部的 class 和 style 合併，形成一個聯合的 class 和 style。

- **v-on 監聽器繼承**：透傳的 v-on 事件監聽器也會被繼承到組件的根元素上，可以與組件內部的監聽器一起使用。

- **深層組件繼承**：當一個組件在根節點上渲染另一個組件時，透傳的 attribute 會傳遞給嵌套的組件。

- **禁用 Attributes 繼承**：如果不希望組件自動繼承 attribute，可以在組件選項中設置 `inheritAttrs: false`，或使用 `<script setup>` 中的 `defineOptions` 來配置。

- **$ attrs 物件**：透傳的 attribute 可以在模板的表示式中直接使用 `$attrs` 來訪問。這個物件包含所有除了組件聲明的 props 和 emits 之外的 attribute。

- **多根節點的 Attributes 繼承**：組件擁有多個根節點時，沒有自動的透傳行為。需要顯式綁定 `$attrs` 才能使用透傳 attribute。

- **在 JavaScript 中訪問透傳 Attributes**：你可以在 `<script setup>` 中使用 `useAttrs()` API 來訪問所有透傳 attribute。如果沒有使用 `<script setup>`，`attrs` 會作為 `setup()` 上下文物件的屬性暴露。

透傳 Attributes 是處理組件與外部環境（父組件）之間的數據傳遞和整合的重要機制，特別適用於控制樣式、事件處理以及其他原生屬性的傳遞。
### 6.插槽
插槽（Slots）是 Vue 元件中非常重要的特性，它允許你將內容插入到元件內部，使元件更加靈活和可重複使用。以下是有關插槽的重點內容：

- **插槽內容與出口**：插槽允許你向元件傳遞模板片段，這些片段將在元件內部渲染。你可以將插槽看作元件的內容容器。插槽內容通常由父元件提供，而插槽出口位於子元件內。

- **插槽的預設內容**：你可以為插槽指定預設內容，以便在沒有提供插槽內容時使用。預設內容會在父元件不提供插槽內容時渲染。

- **具名插槽**：有時候，一個元件需要有多個插槽，這時可以使用具名插槽。你可以為每個插槽指定一個唯一的名稱，並在父元件中為每個插槽傳遞對應的內容。

- **作用域插槽**：作用域插槽允許插槽內容存取父元件的數據，使插槽內容更加動態和靈活。透過在插槽中傳遞 props，插槽可以存取父元件的資料。

- **動態插槽名稱**：你可以使用動態插槽名稱來根據需要切換插槽的名稱。這使你可以在運行時動態選擇要插入的插槽。

- **無渲染元件**：有時，元件可能只包含邏輯而不需要自己渲染內容。這種類型的元件被稱為無渲染元件，它們將視圖渲染工作交給父元件透過插槽來完成。

### 7.依賴注入
提供（provide）和注入（inject）是 Vue.js 中用於解決資料傳遞問題的一種進階模式，通常用於避免逐級透傳 props 的情況。這一模式非常有用，特別是在大型組件樹中，其中的深層組件需要存取距離較遠的資料。

以下是關於提供和注入的重要概念和使用方法：

- **提供資料**：你可以使用 provide 函數來提供資料。通常，在父元件中提供數據，但你也可以在應用程式層級提供數據，以使它在整個應用程式中可用。

- **提供響應式數據**：你可以使用 provide 提供響應式的數據，例如 ref。這允許後代組件與提供者建立響應式連結。

- **應用程式級提供**：你還可以在應用程式層級提供數據，使其在整個應用程式中可用，這對於編寫外掛程式等場景很有用。

- **注入資料**：你可以使用 inject 函數來在元件內部注入提供的資料。你需要指定要注入的資料的名稱。

- **注入預設值**：如果提供者沒有提供數據，你可以指定一個預設值。

- **使用工廠函數**：你可以為預設值使用工廠函數，以延遲計算或初始化操作。這有助於避免不必要的計算。

- **提供/注入響應式資料**：建議將對響應式狀態的變更保留在提供者元件中，以確保狀態的聲明和變更操作都內聚在同一個元件內，從而更容易維護。如果注入方元件需要更改數據，提供者可以提供一個方法函數供注入方呼叫。

- **使用 Symbol 作注入名**：為避免潛在的命名衝突，特別是在大型應用或元件庫中，建議使用 Symbol 作為注入名。通常，你會在一個單獨的檔案中匯出這些 Symbol，以便在供給方和注入方之間共用。



### 8.異步組件
- 使用`defineAsyncComponent`函數創建異步組件，通過載入函數返回`Promise`來實現組件的延遲載入。

- 針對異步組件的載入和錯誤狀態，可以配置載入組件、延遲、錯誤組件、超時限制等高級選項。

- 通常情況下，異步組件與內置的`<Suspense>`組件一起使用，以更好地管理載入和錯誤狀態。

- 異步組件的主要優勢在於提高應用程序的性能，只有在需要時才載入組件，而不必在初始載入時全部載入，從而提高用戶體驗。這對於大型項目和應用程序非常有用。


