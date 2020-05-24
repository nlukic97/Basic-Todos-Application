<template>
  <div class="hello">
    <ul>
      <li>
        <input type="checkbox" v-model="newTask.checked" name="newCheckbox" id="newCheckbox"> <!-- ovo checked nije skroz jasno -->
        <input type="text" v-bind:placeholder="placeholderValues.question" v-on:keyup.enter="addNewTask"  v-model="newTask.description" name="newTask" id="newTask">
        <button v-on:click="removeAllTasks">Clear List</button>
      </li>
      <li v-for="(item, index) in tasks" v-bind:key="index"> 
        <input type="checkbox" v-model="item.checked" name="checkbox" id="checkbox"> <!-- K -->
        <span>{{item.description}}</span>
        <!-- <span>{{item.checked}}</span> -->
        <button v-on:click="removeTask(index)">X</button>
      </li>
    </ul>
    <p>Ako submitujemo bez clicka na prvi checkbox (uopste click), nastane problem.</p>
    <p>Kad onda cekiramo i submitujemo, prikaze se kako treba ali se prvi checkbox ne vraca na unchecked.</p>
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
      //--------------------------------- ima li bolji nacin za ovo? -------------------------------
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
        checked: this.newTask.checked, //ne znam kako da napravim da checkbox bude checked ako je novi checked
      });
      this.newTask.description = '',
      this.newTask.checked = false //to reset the box back to normal
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
    margin:0;
    padding:0;
    li{
      list-style-type: none;
      display:flex;
      justify-content: space-around;
      align-items: center;
      border:1px solid blue;
      background-color: lightblue;
      padding:15px 0;
      &:first-child{
        background-color:gray;
      }
      #newCheckbox, #checkbox {
        width:20px;
        height:20px;
      }

      #newTask{
        border:1px solid #333;
        width:65%;
        padding:10px 10px 10px 10px;
        font-size:14px;
      }
      span {
        width:65%;
        // border:1px solid #333;
        width:65%;
        padding:0 10px;
        font-size:14px;
      }
      // span {
      //   // text-decoration: line-through; //kako da dodajem klasu u vue methods
      // }
    }
  }
}
</style>
