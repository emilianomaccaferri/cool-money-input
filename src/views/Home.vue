<template>
    <div style="display: flex; justify-content: center; align-items: center; height: 100vh; width: 100%;">
      <div id="a">
        <p>{{ str_amount }}€</p>
        <input type="tel" v-model="insertion" id="pog" @input.prevent="check">
      </div> 
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Home',
  data(){
    return {
      amount: 0,
      str_amount: '0,00',
      str_int_amount: '',
      insertion: ''
    }
  },
  mounted(){
    document.getElementById('pog')!.focus();
  },
  methods: {
    check(){

      const last_char = this.insertion.charAt(this.insertion.length - 1);
      if(!/^\d$/.test(last_char)) this.insertion = this.insertion.slice(0, this.insertion.length - 1);

    }
  },
  watch: {
    insertion(value, prev){
      
      const last_char = value.charAt(value.length - 1);
      if(value.length > prev.length) this.str_int_amount += last_char;
      else this.str_int_amount = this.str_int_amount.slice(0, value.length);

      const dec = this.str_int_amount.substring(this.str_int_amount.length, this.str_int_amount.length - 2) || "0";
      const whole = this.str_int_amount.substring(0, this.str_int_amount.length - 2);
      const corrected = (dec.length === 1) ? `0${dec}` : dec;
      
      this.str_amount = `${whole === "" ? '0': Number(whole).toLocaleString('it-IT')},${dec === "" ? '00' : corrected}`;
      console.log(this.str_amount);
      

    }
  }
});
</script>
<style scoped>
#a{
  position: relative;
  display: inline-block;
  margin: 0 auto;
  font-size: 8em;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
#a input{
  position: absolute;
  height: 100%;
  top: 0;
  left: 0;
  width: 90%;
  opacity: 0;
  background: transparent;
  border: none;
  caret-color: transparent; 
  cursor: pointer; 
  outline: none;
}
</style>