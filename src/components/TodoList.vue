
<template >
    
  
  
    <h3 style="margin-top:15px; font-size:32px; text-align: center;"> TO-DO-LIST <hr style="width:300px;"></h3>
   
    <h6 style="font-size:14px ; font-family:Arial, Helvetica, sans-serif; text-align: center; margin-top:-17px;" >created by Mohammad Laal</h6>


    <div class="manage">

   <div class="content">



   <p style="font-size:18px;">New Task</p>
   <p> Task title  <input style="outline: none;"  type="text" v-model="message"  > </p>
    
   <p style="margin-top:10px;">Task time <input style="outline: none;" type="date" v-model="time"> </p>
   <button @click="function1" class="save">Save</button>

   </div>
   
  

   <div class="newtask" >
    <p style="text-align:center;font-size: 18px;">List of tasks</p>
   <p v-for="(message, index) in todolist" :key="index">
    
    
    {{message}}
   
    <button style="float:right; margin-left:10px;" @click="function2(index , message)">Done</button>

    <button style="float:right; " @click="function3(index)">delete</button>

   </p>

  </div>
  
  <div class="found">
     
       <p style=" font-size:19px; text-align: center;">View tasks on the desired date</p>       
    <p style="padding:5px 10px"> Enter the desired date : <input type="date" v-model="search1" @keyup.enter="function7">  </p>
     
     <div v-if="showtext"><p style="padding:5px 10px;"> Your tasks on this date include the following : </p> </div>          
         
    <p style="padding:5px 10px;" v-for="(x , index) in searcharray" :key="index">

     {{x}}
     

    </p>
  </div>

  <button class="done" @click="function4"> done Tasks </button>

  <div class="isactive" v-if="active">

    <p style=" font-size:19px; text-align: center;">List of done tasks</p>
    
<p v-for="(message , index) in tododone" :key="index" > 

{{message}}

<button style="float:right;" @click="function5(index)">delete</button>      

</p>
</div>
</div>
  
 
  </template>
  
  
  <script>
import { yieldExpression } from '@babel/types'

  
  
  export default {



      
    data() {
  
      return { 
      x :'',
      search1 : '' ,
      active : false,
      message : '',
      todolist : [] ,
      time : '',
      todotime : [],
      tododone : [] ,
      searcharray : [] ,
      showtext : false
      
    }
  },
  
   
    methods : {
  
     function1() {
      if( this.message!='' &&  this.time!='') {
      this.todolist.push(this.message)
      localStorage.setItem('to-do' , JSON.stringify(this.todolist))
      this.todotime.push(this.time)
      localStorage.setItem('todotime1' , JSON.stringify(this.todotime))
      this.message = ''
      this.time = ''
    
      }

    } ,


     function2 (index , message) {
      
       this.tododone.push(message)
       localStorage.setItem('to-dodone' , JSON.stringify(this.tododone))
       
        this.todolist.forEach((item , nextItem)=>{
          if(index==nextItem) 
          this.todolist.splice(index , 1)
       })


       localStorage.setItem('to-do' , JSON.stringify(this.todolist))
      
         this.todotime.forEach((item , nextItem)=>{
          if(index==nextItem) 
          this.todotime.splice(index , 1)

       })
       localStorage.setItem('todotime1' , JSON.stringify(this.todotime))
         

     },
     
     function3(index){
  
          this.todolist.forEach((item , nextItem)=>{
            
           if(index==nextItem) 
            this.todolist.splice(index , 1)
           
  
          })
          localStorage.setItem('to-do' , JSON.stringify(this.todolist))

          this.todotime.forEach((item , nextItem)=>{

            if(index==nextItem) 
            this.todotime.splice(index , 1)


          })

         localStorage.setItem('todotime1' , JSON.stringify(this.todotime))

     },

     function4(){

      if (this.tododone!=''){
          
     this.active = true
    }

    else {

    alert("You dont have done task")
    
    }

     },

    function5(index) {
  
      this.tododone.forEach((item , nextItem)=>{
            
            if(index==nextItem) {
             this.tododone.splice(index , 1)
            }
           })

         
   
          localStorage.setItem('to-dodone' , JSON.stringify(this.tododone))

          if (this.tododone == '') {

          this.active=false

          }

    },
    
    function7() {
      this.searcharray=[]
      if(this.search1!='') {
      this.showtext = true  
    for(let i = 0 ; i<this.todotime.length ; i++) {

      if(this.search1 === this.todotime[i]) {
           
      this.x =  this.searcharray.push(this.todolist[i])

      }
     
     
    }
      if(this.searcharray=='') {
    this.showtext=false 
    alert("No task has been registered on this date")

    }
   
  } 
 
}
},
  
   created() {
  
    this.todolist = JSON.parse(localStorage.getItem('to-do') || '[]')
    this.tododone = JSON.parse(localStorage.getItem('to-dodone') || '[]')
    this.todotime = JSON.parse(localStorage.getItem('todotime1') || '[]')
    
  },
  
  
  }
 
  
  </script>
  
  <style>
  
  * {

  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;

  }
  

  
  .content {
  
  margin-top: 50px;
  
  border:2px solid orange ;
  width: 200px;
  padding: 3px 5px;
  text-align: center;
  position: relative;
  left: 120px;
  }

  .manage {
   
    margin-left: 540px;

  }

  .done {

   position:relative ;
   left: 140px;
   text-align: center;
   cursor: pointer;
   width: 200px;
   height: 50px;
   background-color: green;
   border: none;
   margin-top: 20px;
   
   border-radius: 10px;
  }

  .isactive {
   margin-top: 30px;
   min-width: 250px;
   max-width: 450px;
   min-height: 100px;
   border: 2px solid rgb(230, 79, 24);
   position: relative;
   padding:5px 20px;
  
}

  .save {

   margin-top: 5px;
   margin-right: 5px;
   border: none;
   border-radius: 5px;
   background-color: rgb(55, 54, 54);
   color: white;
   padding: 6px 20px;
  
  }

  .newtask {

  border:2px solid orange;
  min-width: 250px;
  max-width: 450px;
  margin-top:20px;
  padding: 0px 10px;

}
  
  .found {
   margin-top: 30px;
   border:2px solid orange;
   min-width: 250px;
   max-width: 450px;
}



</style>