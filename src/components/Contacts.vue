<template>
  <div class="contacts">
    <input type="text" id="name" v-model="name">
    <input type="text" id="email" v-model="email">
    <button v-on:click="addContact">ADD</button>
    <div id="contacts">
      <div class="contact" v-for="contact in contacts" v-bind:key="contact.email">
        <h2>{{contact.name}} {{contact.email}} {{contact.contacted}}</h2>

      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Contacts',
  props: {
    msg: String
  },
  data(){
    return{
      contacts: []
    }
    
  },
  methods:{
    addContact() {
      const cont = this.contacts.find(cont => cont.email === this.email);
      if(typeof cont == "undefined"){
        const contact = {};
        contact.name = this.name;
        contact.email = this.email;
        contact.contacted = false;
        this.contacts.push(contact);
      }else{
        alert("Email repetido");
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
