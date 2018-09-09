<template>
  <div class="container h-100 d-flex justify-content-center" id="regBox">
    <div v-if="hidetable == 1" v-cloak>
      <template>
        <div class="col-md-12">
          <label>Please select the required datafields of the table</label>
          <b-form-checkbox-group v-model="fieldselect" :options="selections" class="mb-3" aria-required="required"></b-form-checkbox-group>
        </div>
      </template>
      <div class="px-3">
        <b-button :size="'sm'" :variant='"primary"' @click="showdata" :class="{ disabled: isDisabled }" :disabled="isDisabled">Submit</b-button>
      </div>
    </div>
    <div v-if="hidetable == 2" v-cloak>
      <div class="justify-content-centermy-1 row">
        <b-form-fieldset horizontal label="Rows per page" class="col-6">
          <b-form-select :options="[{text:5,value:5},{text:10,value:10},{text:15,value:15}]" v-model="perPage">
          </b-form-select>
        </b-form-fieldset>

        <b-form-fieldset horizontal label="Filter" class="col-6">
          <b-form-input v-model="filter" placeholder="Type to Search"></b-form-input>
        </b-form-fieldset>
        <div class="px-3">
          <b-button :size="'sm'" :variant="'primary'" @click="backtostart"> Go Back </b-button><br>
        </div>
      </div>
      <template>
        <b-table striped hover :items="items" :fields="fields" :current-page="currentPage" :per-page="perPage" :filter="filter"></b-table>
      </template>
      <div class="justify-content-center row my-1">
        <b-pagination size="md" :total-rows="this.items.length" :per-page="perPage" v-model="currentPage" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      disableButton: true,
     fields: {},
      fieldselect:[],
      selected: [], // Must be an array reference!
       
       selections: [
         { value: 'first', text: 'Name' },
         {value: 'age', text: 'Age'},
         {value: 'sex', text: 'Sex'},
         {value: 'email', text: 'Email'},
         {value: 'phone', text: 'Phone'}
       ],
      items:[
        { age: 40, name: 'Dickerson',sex:'Male', email:'dicke@gmail.com', phone:'9523648963'},
        { age: 21, name: 'Larsen',sex:'Male',email:'lar@gmail.com', phone:'4563214589' },
        { age: 89, name: 'Geneva',sex:'Female',email:'cod@gmail.com', phone:'9632541236' },
        { age: 38, name: 'Jami',sex:'Female',email:'jami@gmail.com', phone:'5412365478' },
        { age: 24, name: 'Allen',sex:'Male',email:'allenshaji10@gmail.com', phone:'8547933472'},
        { age: 21, name: 'Anoop',sex:'Male',email:'scty@gmail.com', phone:'9632587415' },
        { age: 29, name: 'Sobin',sex:'Male',email:'yorker@gmail.com', phone:'9874563219' },
        { age: 28, name: 'Mathew',sex:'Male',email:'manager@gmail.com', phone:'7896325419' },
      ],
      fselect:'',
      hidetable: 1,
      currentPage: 1,
      perPage: 5,
      filter: null
       }
     },
       computed: {
       isDisabled () {
       if (this.fieldselect.length > 0) {
        return false;
       } else {
        return true;
           }
           }
          },
          watch:{
          fieldselect: function() {
            var vm = this;
            var fieldinst = this.fieldselect;
            if(fieldinst.indexOf('first')>=0){
                vm.fields.name={label: 'Name', sortable: true};
            }else{
                delete vm.fields.name;
            } 
            if(fieldinst.indexOf('age')>=0){
                vm.fields.age={label: 'Age', sortable: true};
            }else{
                delete vm.fields.age;
            } 
            if(fieldinst.indexOf('sex')>=0){
                vm.fields.sex={label: 'Sex', sortable: true};
            }else{
                delete vm.fields.sex;
            } 
            if(fieldinst.indexOf('email')>=0){
                vm.fields.email={label: 'Email', sortable: true};
            }else{
                delete vm.fields.email;
            } 
            if(fieldinst.indexOf('phone')>=0){
                vm.fields.phone={label: 'Phone', sortable: true};
            }else{
                delete vm.fields.phone;
            } 
        }

        },
        methods: {
          showdata: function(){
            var vm = this;
            vm.hidetable=2;
            vm.hello=1;
        },
        backtostart: function(){
            var vm = this;
            vm.hidetable=1;
            vm.btn=8;
            vm.fselect='';
            vm.fieldselect=[];
            vm.selected=[];
            vm.fields={};
        },
    handelSubmit: function(e) {
      var vm = this;
      
      vm.items = this.items;
},
},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
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
