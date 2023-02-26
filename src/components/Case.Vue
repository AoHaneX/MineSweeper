<template>

  <button v-show="hide==false" @click="reveal(Case)">&#127761;</button>


</template>

<script>
export default {
name: 'HelloWorld',
methods: {
test(){
console.log('Data received:',"1");
},
reveal(Case){
Case.hide=true;
}
},
props:{ 
newCase: { type: Object }
},

data() {
return {

}
}

}
</script>
