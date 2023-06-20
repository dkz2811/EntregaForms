<template>
    <div >
      <table class="table">
        <thead>
          <th>name</th><th>email</th><th>nationality</th>
        </thead>
        <tr class="table-row"  v-for="(user,i) in users" :key="user.email">
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.nationality }}</td>
          <td>
            <label :for="user.email">{{ label }}</label>
            <select :id="user.email" @input="inputHandler($event, i)">
              <option v-for="option in options" 
                      :key="option.value" 
                      :value="option.value">
                      {{ option.name }}
              </option>
            </select>
            </td>
          <td>
              <button class="btn btn-danger" @click="clickHandler(i,'delete')">Delete</button>
          </td>
        </tr>
      </table>
    </div>
  </template>
<script>
export default {
    name: "TabComp.vue",
    props:{
        users:{
          type: Array,
          required: true
        },
        id:{
          type:String,
          required:true
        },
        value:{
          type:String,
          required: false
        },
        label:{
          type:String,
          required:true
        },
        options:{
          type:Array,
          required:true
        },
    },
    data(){
      return {
        userList:[],
        checks:[]
      }
    },
    methods:{
      clickHandler(pos,str){
        if(str==='delete'){
          this.deleteUser(pos)
        }else if( str === 'update'){
          this.updateUser(pos)
        }
      },
      deleteUser(pos){
          this.userList = this.users.slice();
          this.userList.splice(pos,1)
          this.$emit('updateList', this.userList)
      },
      editUser(user){
        console.log(user)
      },
      inputHandler(event,pos){
        let user = {}
        user.name = this.users[pos].name
        user.email = this.users[pos].email
        user.password = this.users[pos].password        
        user.nationality = event.target.value;
        this.userList = this.users.slice();
        this.userList.splice(pos,1, user)
        this.$emit('updateList',this.userList)
      }
    }
}
</script>
<style>
    
</style>