<script setup>
import { ref } from 'vue'
let icon = ref(true)
let openAdd = ref(false)
let previous = ref(false)
let noteAppsave = ref([])

// function edit(){
  
// }


function openAddButton(){
  openAdd.value = true
  
}
function closeAddButton() {
  openAdd.value = false
}


function openPrev(){
  icon.value = false
  previous.value = true
}


let title = ref('')
let description = ref('')


function addNote(){
  const object = {
    noteTitle:title.value,
    noteDescription:description.value,
    currentDate: new Date,
    id: Math.floor(Math.random() * 20)
  }
  console.log(object.id);
  noteAppsave.value.push(object)
  title.value = ''
  description.value = ''
  closeAddButton()
  openPrev() 
}

function removeDoc(id){
  console.log(id);
  noteAppsave.value = noteAppsave.value.filter(item =>{
    return item.id !== id
  }

  )
}


</script>
<template>
  <div class="slide" style="background-color: rgba(247,247,247,255);">
    <header>
      <div class="logo">
        <p>TEMMIE SMIL😉S</p>
      </div>
      <nav>
        <acronym  class="acronym" title="ADD NOTE">
        <img @click="openAddButton()" src="../img/pngaaa.com-5253318.png" alt="">
        </acronym>
      </nav>
    </header>
    <div class="center-note-text" v-if="openAdd">
      <div class="add-note-div">
      <p>keep your note save with us</p>
      <div class="input-and-text">
        <input type="text" placeholder="note title" v-model="title">
        <textarea  placeholder="input your note" name="note" id="" cols="30" rows="10" v-model="description"></textarea>
      </div>
      <div class="buttons">
        <button @click="addNote()">create</button>
        <button @click="closeAddButton()">close</button>
      </div>
    </div>
    </div>
    <div>
      <div class="detail"  v-if="icon">
        <div>
        <acronym title="Show Previous Note"><img @click="openPrev()" src="../img/one-note-xxl.png" alt=""> </acronym>
        </div>
        <p>....Keeping Your Note And Document Save....</p>
      </div>
    </div>
    
      <div class="center" v-if="previous">
        <div class="grid-items"  v-for="note in noteAppsave" :key="id"> 
          <p class="titl">{{ note.noteTitle }}</p>
          <hr>
          <p class="none"> {{ note.noteDescription }} </p>
          <div class="del"><p>{{ note.currentDate.toLocaleDateString() }}</p> <div><img class="icon-pic" src="../img/edit.png" alt=""> <img @click="removeDoc(note.id)" class="icon-pic" src="../img/trash-bin.png" alt=""></div> </div>
        </div>

        <div class="toast">
          <p class="notice"></p>
          <font-awesome-icon icon="fa-solid fa-check" />
          <font-awesome-icon icon="fa-solid fa-xmark" />
        </div>
      </div>
  </div>
</template>

<style scoped>

.toast{
  position: absolute;
  /* border: 2px solid red; */
  width: 300px;
  height: 50px;
}
header{
  justify-content: space-between;
  align-items: center;
  display: flex;
  padding: 20px;
  border-bottom-right-radius: 10px;
  border-bottom-left-radius: 10px;
  border-bottom: 4px solid rgba(0,135,247,255);
  margin-top: 2px;
  margin-left: 10px;
  margin-right: 10px;
  box-shadow: 0px 4px 12px 1px rgba(0,0,0,0.71);
-webkit-box-shadow: 0px 4px 12px 1px rgba(0,0,0,0.71);
-moz-box-shadow: 0px 4px 12px 1px rgba(0,0,0,0.71);

}


header nav img{
  width: 70px;
  height: 70px;
  }

.logo p{
background-color:rgba(0,135,247,255);
color: white;
font-size: 25px;
font-weight: bolder;
font-style: italic;
padding: 10px 10px;
border-radius: 10px;
}


.detail{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  font-size: 30px;
  gap: 10px;
  color: rgba(0,135,247,255);
  height: 80vh;
  font-weight: bolder;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-style: italic;
}




.detail div{
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  opacity: 0.3;
  transition: 0.7s ease-in-out;
}
.detail div:hover{
  opacity: 1;
}
.detail img{
  height: 150px;
}

.detail p{
  font-size: 17px;
  opacity: 0.3;
}

.add-note-div{
  display: flex;
  flex-direction: column;
  margin: 10px;
  margin-bottom: 30px;
  width: 150vh;
  background-color: white;
  border-radius: 10px;
  box-shadow: 0px 0px 10px -2px rgba(0,0,0,0.59);
-webkit-box-shadow: 0px 0px 10px -2px rgba(0,0,0,0.59);
-moz-box-shadow: 0px 0px 10px -2px rgba(0,0,0,0.59);

	-webkit-animation: slide-fwd-bottom 0.75s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
	        animation: slide-fwd-bottom 0.75s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;

}


@-webkit-keyframes slide-fwd-bottom {
  0% {
    -webkit-transform: translateZ(0) translateY(0);
            transform: translateZ(0) translateY(0);
  }
  100% {
    -webkit-transform: translateZ(80px) translateY(30px);
            transform: translateZ(80px) translateY(30px);
  }
}
@keyframes slide-fwd-bottom {
  0% {
    -webkit-transform: translateZ(0) translateY(0);
            transform: translateZ(0) translateY(0);
  }
  100% {
    -webkit-transform: translateZ(80px) translateY(30px);
            transform: translateZ(80px) translateY(30px);
  }
}

.add-note-div p{
  margin-top: 10px;
  font-size: 30px;
  font-family: sans-serif;
  font-weight:bolder ;
  color: rgba(0,135,247,255);
  text-transform: capitalize;
  text-decoration: underline;
  font-style: italic;
  text-align: center;
}
.input-and-text{
  display: flex;
  flex-direction: column;
  gap: 10px;
  justify-content: center;
  padding: 20px;
}

.input-and-text input{
  font-size: 20px;
  color:rgba(0,135,247,255);
  height: 40px;
  border-radius: 5px;
  outline: none;
  border: none;
  border-bottom: 2px solid rgba(0,135,247,255);
  border-right: 2px solid rgba(0,135,247,255);
}

.input-and-text input::placeholder{
  color: rgba(0,135,247,255);
  text-transform: uppercase;
  font-size: 18px;
}

textarea{
  font-size: 20px;
  color:rgba(0,135,247,255);
  max-width: 100%;
  resize: vertical;
  min-height: 150px;
  border-radius: 5px;
  outline: none;
  border: none;
  border-bottom: 2px solid rgba(0,135,247,255);
  border-right: 2px solid rgba(0,135,247,255);
}

.input-and-text textarea::placeholder{
  color: rgba(0,135,247,255);
  text-transform: uppercase;
  font-size: 18px;
}
.buttons{
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;  
  margin-bottom: 10px;
}

.center-note-text{
display: flex;
justify-content: center;
padding: 0 50px;
}

button{
  color: white;
  background-color: rgba(0,135,247,255);
  border: none;
  font-size: 20px;
  text-transform: capitalize;
  font-weight: bold;
  padding: 10px;
  width: 150px;
  border-radius: 10px;
}

.center{
  display: grid;
  /* grid-template-columns: 1fr 1fr 1fr; */
  grid-template-columns: repeat(auto-fit,minmax(400px ,1fr));
  place-items: center;
  gap: 20px;
  padding: 20px;
  -webkit-animation: swing-in-top-fwd 0.7s cubic-bezier(0.175, 0.885, 0.320, 1.275) both;
	        animation: swing-in-top-fwd 0.7s cubic-bezier(0.175, 0.885, 0.320, 1.275) both;
}

.del{
  /* margin-top: 10px; */
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.del p{
  font-size: 20px;
}


@-webkit-keyframes swing-in-top-fwd {
  0% {
    -webkit-transform: rotateX(-100deg);
            transform: rotateX(-100deg);
    -webkit-transform-origin: top;
            transform-origin: top;
    opacity: 0;
  }
  100% {
    -webkit-transform: rotateX(0deg);
            transform: rotateX(0deg);
    -webkit-transform-origin: top;
            transform-origin: top;
    opacity: 1;
  }
}
@keyframes swing-in-top-fwd {
  0% {
    -webkit-transform: rotateX(-100deg);
            transform: rotateX(-100deg);
    -webkit-transform-origin: top;
            transform-origin: top;
    opacity: 0;
  }
  100% {
    -webkit-transform: rotateX(0deg);
            transform: rotateX(0deg);
    -webkit-transform-origin: top;
            transform-origin: top;
    opacity: 1;
  }
}




.grid-items{
  background-color: #fff;
  color: rgba(0,135,247,255);
  border: 4px solid rgba(0,135,247,255);
  height: 15em;
  width: 400px;
  padding: 3px 10px 10px 10px ;
  border-radius: 20px;
  -webkit-animation: slide-in-fwd-left 0.4s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
	        animation: slide-in-fwd-left 0.4s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
}

hr{
  color: rgba(0,135,247,255);
  background-color: rgba(0,135,247,255);
  height: 4px;
}
@-webkit-keyframes slide-in-fwd-left {
  0% {
    -webkit-transform: translateZ(-1400px) translateX(-1000px);
            transform: translateZ(-1400px) translateX(-1000px);
    opacity: 0;
  }
  100% {
    -webkit-transform: translateZ(0) translateX(0);
            transform: translateZ(0) translateX(0);
    opacity: 1;
  }
}
@keyframes slide-in-fwd-left {
  0% {
    -webkit-transform: translateZ(-1400px) translateX(-1000px);
            transform: translateZ(-1400px) translateX(-1000px);
    opacity: 0;
  }
  100% {
    -webkit-transform: translateZ(0) translateX(0);
            transform: translateZ(0) translateX(0);
    opacity: 1;
  }
}



.icon-pic{
  height: 30px;
  width: 30px;
}

.titl{
  font-size:20px;
  font-weight: bolder;
  height: 10%;
  margin-bottom: 4px;

}

.none{
  word-wrap: break-word;
  height: 75%;
  border-bottom: 1px solid rgba(0,135,247,255);
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  overflow-y: scroll;
  /* transition: 2s ease-in-out; */
}

.none::-webkit-scrollbar{
  width:3px;
  height: 10px;
}
.none:hover::-webkit-scrollbar{
  width:5px;
  height: 10px;
}

.none::-webkit-scrollbar-track{
  background-color: transparent;
  border-radius: 5px;
  margin:10px 0;
}
.none::-webkit-scrollbar-thumb{
  background-color: transparent;
  border-radius: 20px;
}
.none:hover::-webkit-scrollbar-thumb{
  background-color: rgba(0,135,247,255);
  border-radius: 20px;
}

@media (max-width:451px) {
    .logo p{
        font-size: 16px;
    }
    .add-note-div p{
      font-size: 20px;
    }

    .add-note-div{
      width: 40vh;
    }

    .center{
      padding:20px;
      grid-template-columns: 1fr ;
    }
    button{
      width: 100px;
    }
    .grid-items{
      width: 80%;
      height: 12em;
    }
    header nav img{
      width: 50px;
      height: 50px;
    }

    .detail p{
      font-size: 14px;
    }
    .detail img{
      width: 100px;
      height: 140px;
    }

}

@media (max-width:301px){
  .logo p{
        font-size: 13px;
        padding: 7px;
    }

    header nav img{
      width: 30px;
      height: 30px;
    }

    .detail p{
      font-size: 10px;
    }
    .detail img{
      width: 70px;
      height: 100px;
    }
    .add-note-div p{
      font-size: 14px;
    }
    .add-note-div{
      width: 35vh;
    }
    button{
      width: 70px;
      font-size: 16px;
    }
}



</style>