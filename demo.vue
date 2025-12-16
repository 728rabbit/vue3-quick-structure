/*
Count.js
export default {
  data() {
    return {
      count: 0,
    };
  },
  methods: {
    incrementCount() {
      this.count += 1;
    },
  },
}; 
*/

<script>
import { ref, reactive, computed, watch, onMounted, onBeforeUnmount, onUpdated } from 'vue';

// import Count from './Count';

export default {
  // ==============================
  // 元件名稱 (可選)
  // ==============================
  name: 'MyComponent', // 組件名稱，方便 DevTools 或調試

  // ==============================
  // 父組件傳入的 props
  // ==============================
  props: {
    title: {
      type: String,        // 資料型別
      required: true,      // 是否必填
      default: 'Hello',    // 預設值
      validator: (value) => value.length > 0 // 自訂驗證
    },
    count: {
      type: Number,
      default: 0
    }
  },

  // 使用 Composition 宣告變數要用 ref 來初始化，而這個 ref 必須要先 import 才可以使用。
  // 使用 setup() {} 把變數放在此內部。
  // 如果要宣告結構變數的話就必須要使用 reactive ，然後將變數放在裡面，而初始化的時候就不用 ref 了
  // Composition API 幾乎可以完全取代 mixins，而且還更安全、更清楚。
  setup() {
    const name = ref('');
    name.value = 'Jake';

    const user = reactive({
      id: 0,
      name: '',
    });
    user.id = 1;
    user.name = 'Allan';
    
    return {
      name, user
    };
  },

  // ==============================
  // 組件內部資料 (data)
  // ==============================
  data() {
    return {
      message: 'Hello Vue3', // 普通資料
      loading: false          // 控制 UI 狀態
    };
  },

  // ==============================
  // 計算屬性 (computed)， 只運行一次
  // ==============================
  computed: {
    doubleCount() {
      return this.count * 2; // 依賴 props 或 data
    }
  },

  // ==============================
  // 監聽器 (watch)
  // ==============================
  watch: {
    count(newVal, oldVal) {
      console.log('count changed:', oldVal, '->', newVal);
    },
    // 深層監聽 reactive 對象
    message: {
      handler(newVal) {
        console.log('message changed:', newVal);
      },
      immediate: true, // 初始化時也執行一次
      deep: true       // 深層監聽
    }
  },

  // ==============================
  // 方法 (methods)
  // ==============================
  methods: {
    increment() {
      this.count += 1;
    },
    async fetchData() {
      this.loading = true;
      try {
        const res = await fetch('/api/data');
        const data = await res.json();
        this.message = data.msg;
      } catch (err) {
        console.error(err);
      } finally {
        this.loading = false;
      }
    }
  },

  // ==============================
  // 組件生命週期 (Lifecycle hooks)
  // ==============================
  beforeCreate() {
    console.log('beforeCreate: 還沒初始化 data & props');
  },
  created() {
    console.log('created: data & props 已可使用，但 DOM 還沒渲染');
  },
  beforeMount() {
    console.log('beforeMount: template 還沒插入 DOM');
  },
  mounted() {
    console.log('mounted: DOM 已渲染完成');
  },
  beforeUpdate() {
    console.log('beforeUpdate: data 更新但 DOM 還沒更新');
  },
  updated() {
    console.log('updated: DOM 已更新');
  },
  beforeUnmount() {
    console.log('beforeUnmount: 組件即將被銷毀');
  },
  unmounted() {
    console.log('unmounted: 組件已被銷毀');
  },

  // ==============================
  // 元件可用的組件 (子組件)
  // ==============================
  components: {
    // MyChildComponent
  },

  // ==============================
  // 指令 (Directives)
  // ==============================
  directives: {
    focus: {
      mounted(el) {
        el.focus(); // 元素掛載時自動 focus
      }
    }
  },

  // ==============================
  // 混入 (Mixins)
  // ==============================
  mixins: [
    // someMixin, e.g: Count
  ],

  // ==============================
  // 提供給子組件 / 注入 (provide / inject)
  // ==============================
  provide() {
    return {
      someData: this.message
    };
  },
  inject: ['parentData'],

  // ==============================
  // 自訂事件 (emits), 通常子傳給父組件數值
  // ==============================
  emits: ['update', 'delete'],

  // ==============================
  // 過濾器 (Filters) Vue2 有，Vue3 不推薦
  // ==============================
  // filters: {
  //   uppercase(value) {
  //     return value.toUpperCase();
  //   }
  // }
};
</script>
