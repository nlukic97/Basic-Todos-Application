<template>
  <div class="hello">
    <ul>
      <li>
        <input type="checkbox" v-model="newTask.checked" name="newCheckbox" id="newCheckbox"> <!-- ovo checked nije skroz jasno, pogledaj jos koji put -->
        <input type="text" v-bind:placeholder="placeholderValues.question" v-on:keyup.enter="addNewTask"  v-model="newTask.description" name="newTask" id="newTask">
        <button id="clearAllBtn" v-on:click="removeAllTasks">Clear List</button>
      </li>
      <li v-for="(item, index) in tasks" v-bind:key="index"> 
        <input type="checkbox" v-model="item.checked" name="checkbox" id="checkbox"> <!-- K -->
        <span>{{item.description}}</span>
        <!-- is it checked or not status - uncomment code underneath to check -->

        <!-- <span>{{item.checked}}</span> --> 
        <button id="removeTaskBtn" v-on:click="removeTask(index)">&#10060;</button>
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
          description:'Task 2 - checked',
          checked:true
        },
        {
          description:'Task 1 - not checked',
          checked: false
        }
      ],
      newTask:[{
        description:'',
        checked:''
      }],
      placeholderValues:{
        question:'What do you need to do?'
      }
    }
  },
  methods:{
    addNewTask: function(){
      //--------------------------------- ima li bolji nacin za ovo, tj mora li uopste?-------------
      if(this.newTask.checked){
        console.log('checked');
        this.newTask.checked = true;
      }   else {
        console.log('Not checked');
        this.newTask.checked = false ; //ovo stavljeno jer na prvi submit bez clicka na input, ne salje nista u newTask (nema false)
      }
      //---------------------------------------------------------------------------------------------
      this.tasks.unshift({
        description: this.newTask.description,
        checked: this.newTask.checked
      });
      this.newTask.description = '',
      this.newTask.checked = false //to reset the box back to normal - ima bug
    },
    removeTask: function(taskIndex){
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
  border: 1px solid #a5a2a2;
  margin:15px 60px 0 60px;
  ul{
    overflow: hidden;
    margin:0px;
    padding:0;
    li{
      list-style-type: none;
      display:flex;
      justify-content: space-around;
      align-items: center;
      background-color: #3564A4;
      padding:15px 0;
      margin:0 0 1px 0;
      &:first-child{
        background-color:#E7E8EB;
        margin:0px;
        z-index:1;
        position: relative;
        #newTask{
          border:1px solid #333;
          width:65%;
          padding:15px 10px 15px 10px;
          font-size:14px;
        }
        #clearAllBtn {
          padding:12px 20px;
          font-size: 18px;
          color:#333;
          background-color:#fff;
          border:1px solid #a5a2a2;
        }
      }
      &:last-child{
        margin:0px;
      }
      #removeTaskBtn {
        opacity:0%;
        transition:0.3s opacity;
        margin:10px 10px 10px 74px;
        background-color:#3564A4;
        border:none;
        font-size:20px;
        &:hover{
            cursor:pointer;
          }
      }
      &:hover #removeTaskBtn{
          opacity:100%;
        }
      #newCheckbox, #checkbox {
        width:20px;
        height:20px;
      }
      span {
        width:65%;
        padding:0 10px;
        font-size:14px;
        color:#DDE2EC;
        text-align: left;
        font-size:25px;
      }
      // span {
      //   // text-decoration: line-through; //kako da dodajem klasu u vue methods ako je checkbox checked
      // }
    }
  }
}
</style>
