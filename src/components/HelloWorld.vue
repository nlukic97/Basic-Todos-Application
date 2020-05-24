<template>
  <div class="hello">
    <ul>
      <li>
        <input type="checkbox" name="selectAll" id="selectAll">
        <input type="text" v-bind:placeholder="placeholderValues.question" v-on:keyup.enter="addNewTask"  v-model="newTask.description" name="newTask" id="newTask">
        <button v-on:click="removeAllTasks">Clear List</button>
      </li>
      <li v-for="(item, index) in tasks" v-bind:key="index"> <!--Nije najjasnije sve ovde, konkretno ovo bind -->
        <input type="checkbox" v-on:click="removeTask(index)" name="clear" id="clear">
        <span>{{item.description}}</span>
        <button v-on:click="removeTask(index)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: function(){
    return {
      tasks:[{
          description:'Do this and that'
        },
        {
          description:'Do this again but for 2'
        }
      ],
      newTask:[{
        description:''
      }],
      placeholderValues:{
        question:'What do you need to do?'
      }
    }
  },
  methods:{
    addNewTask: function(){
      this.tasks.unshift({
        description: this.newTask.description
      });
      this.newTask.description = ''; //to clear input on enter
    },
    removeTask: function(taskIndex){ //Zasto se cekira odmah ispod opcija nakon sto prva nestane?
      this.tasks.splice(taskIndex, 1);
      
    },
    removeAllTasks: function(){
        this.tasks.splice(0,this.tasks.length);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello {
  border:1px solid red;
  ul{
    li{
      list-style-type: none;
      display:flex;
      justify-content: space-around;
    }
  }
}
</style>
