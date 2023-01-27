
<template>
  <div class="modal-overlay">
    <div class="modal">
        <div div>{{text}}</div>
      <div class="button-wrapper">
        <button class="margin-buttom" @click="confirmed">Confirm</button>
        <button class="margin-buttom" @click='closeModal'>Batal</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Dialogs",
  props: {
    text: {
      type: String,
      default: ""
    },
    value: {
      type: Boolean,
    }
  },  
  watch: {
    value: function() {
      this.$emit('update', this.value)
    }
  },  
  methods: {
    closeModal() {
      this.$emit('cancel', {hi: 'from child!'})
    },
    confirmed() {
      this.$emit('confirm', 30)
    }
  }
}
</script>

<style>
.modal-overlay {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
    background-color: #000000da;
  }
  .modal {
    text-align: center;
    background-color: white;
    height: 50px;
    width: 300px;
    margin-top: 10%;
    padding: 60px 0;
    border-radius: 20px;
  }
  
  .margin-buttom {
    margin-left: 3px;
    margin-right: 3px;
  }

  .button-wrapper {
    margin-top: 10px;
  }
</style>