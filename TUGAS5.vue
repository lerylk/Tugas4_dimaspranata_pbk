<script>
export default {

  // LIFECYCLE HOOK
 
  mounted() {
    console.log('Komponen telah dimuat!')
    this.initTime = new Date().toLocaleTimeString()
    this.$refs.itemInput.focus()
  },

  data() {
    return {
    
      items: [],
      inputText: '',
      
      
      lastChange: '',
      initTime: null
    }
  },

  // COMPUTED PROPERTIES
  
  computed: {
    totalItems() {
      return this.items.length
    },
    isInputEmpty() {
      return this.inputText.trim() === ''
    },
    inputStatus() {
      return this.isInputEmpty ? 'Input Kosong' : 'Input Terisi'
    }
  },

  // WATCHERS

  watch: {
    items: {
      handler(newVal) {
        this.lastChange = `Daftar diupdate: ${new Date().toLocaleTimeString()}`
        console.log('Items berubah:', newVal)
      },
      deep: true
    },
    inputText(newVal) {
      this.lastChange = `Input diubah: ${newVal} (${new Date().toLocaleTimeString()})`
    }
  },

  // METHODS & TEMPLATE REFS
  methods: {
    addItem() {
      if (!this.isInputEmpty) {
        this.items.push(this.inputText)
        this.inputText = ''
        this.$refs.itemInput.focus()
      }
    },
    focusInput() {
      this.$refs.itemInput.focus()
      this.$refs.itemInput.style.border = '2px solid #42b883'
      setTimeout(() => {
        this.$refs.itemInput.style.border = ''
      }, 1000)
    }
  }
}
</script>

<template>
  <div id="app">
    <section class="feature-box">
      <h2>1. Input Data & List Rendering</h2>
      <input 
        ref="itemInput" 
        v-model="inputText" 
        placeholder="Ketik item baru"
        @keyup.enter="addItem"
      >
      <button 
        :disabled="isInputEmpty" 
        @click="addItem"
      >
        Tambah Item
      </button>

      <ul class="item-list">
        <li v-for="(item, index) in items" :key="index">
          {{ item }}
        </li>
      </ul>
    </section>

    
    <section class="feature-box">
      <h2>2. Computed Properties</h2>
      <p>Jumlah Item: {{ totalItems }}</p>
      <p>Status Input: {{ inputStatus }}</p>
    </section>

    
    <section class="feature-box">
      <h2>3. Watchers</h2>
      <p>Perubahan Terakhir: {{ lastChange }}</p>
    </section>

    
    <section class="feature-box">
      <h2>4. Template Refs</h2>
      <button @click="focusInput">
        Fokus ke Input
      </button>
    </section>

   
    <section class="feature-box">
      <h2>5. Lifecycle Hook</h2>
      <p>Waktu Inisialisasi: {{ initTime }}</p>
    </section>
  </div>
</template>
