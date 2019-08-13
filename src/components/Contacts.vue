<template>
  <div class="contacts">
    <input type="text" id="name" v-model="name">
    <input type="text" id="email" v-model="email">
    <button v-on:click="addContact">ADD</button>
    <br>
    <button v-on:click="deletedAll">Delete ALL</button>
    <button v-on:click="allContacted">Contacted ALL</button>
    <button v-on:click="showOnlyContacted">Show Only Contacted</button>

    <div id="Allcontacts" v-if="!onlyContacted">
      <div class="contact" v-for="contact in contacts" v-bind:key="contact.email">
        <div class="contactedTrue" v-if="contact.contacted">
          <h2>Name: {{contact.name}} Email: {{contact.email}} Contacted: {{contact.contacted}}</h2>
          <button v-on:click="editContact(contact.email)">Edit</button>
          <button v-on:click="deletedContact(contact.email)">Delete</button>
          <input v-on:click="contacted(contact.email)" type="checkbox" checked>
        </div>
        <div class="contactedFalse" v-if="!contact.contacted">
          <h2>Name: {{contact.name}} Email: {{contact.email}} Contacted: {{contact.contacted}}</h2>
          <button v-on:click="editContact(contact.email)">Edit</button>
          <button v-on:click="deletedContact(contact.email)">Delete</button>
          <input v-on:click="contacted(contact.email)" type="checkbox">
        </div>

      </div>
    </div>
    <div id="Onlycontacts" v-if="onlyContacted">
      <div class="contact" v-for="contact in contacts" v-bind:key="contact.email">
        <div class="" v-if="contact.contacted">
          <h2>Name: {{contact.name}} Email: {{contact.email}} Contacted: {{contact.contacted}}</h2>
          <button v-on:click="editContact(contact.email)">Edit</button>
          <button v-on:click="deletedContact(contact.email)">Delete</button>
          <input v-on:click="contacted(contact.email)" type="checkbox" checked>
        </div>
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
      contacts: [],
      onlyContacted: false
    }
    
  },
  methods:{
    addContact() {
      const cont = this.contacts.find(cont => cont.email === this.email);
      if(typeof cont == "undefined"){
        console.log(this.name.length);
        if(this.name.length >= 6){

          const contact = {};
          contact.name = this.name;
          contact.email = this.email;
          contact.contacted = false;
          return this.contacts.push(contact);
        }else{
          return alert("The name must have more than 6 letters");
        }  
      }else{
        return alert("Email repeated");
      }
    },
    editContact(email){
      const contact = this.contacts.find(cont => cont.email === email);
      const repeatedContact = this.contacts.find(cont => cont.email === this.email);
      if(typeof repeatedContact != 'undefined'){
        contact.email = this.email;
        contact.name = this.name;
        return contact;
      }else{
        return alert("Email repeated");
      }

    },
    deletedContact(email){
      const index = this.contacts.findIndex(cont => cont.email === email);
      this.contacts.splice(index, 1);
    },
    contacted(email){
      const contact = this.contacts.find(cont => cont.email === email);
      contact.contacted = !contact.contacted;
    },
    showOnlyContacted(){
      console.log(this.onlyContacted);
      
      this.onlyContacted = !this.onlyContacted;
    },
    deletedAll(){
      this.contacts = [];
    },
    allContacted(){
      this.contacts.forEach(cont => {
        cont.contacted = true;
      });
      
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
