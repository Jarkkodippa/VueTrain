<template>
  <div>
    <Notesboard />
  </div>
</template>

<script>
import Notesboard from "./components/Notesboard";
export default {
  name: "App",
  components: {
    Notesboard,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: black;
  margin-top: 60px;
}

table.totTable {
  vertical-align: top;
  padding: 10px;
  margin: 10px;
  width: 500px;
  border: 1px solid #0d0e0d;
  background-color: rgb(255, 255, 255);
}


table.resultTable {
  width:1000px; 
  border-collapse: collapse;
  border: solid 1px #777;
}


div.resultDiv {
  padding: 10px;
  margin: 10px;
  width: 1000px;
  border: 1px solid #0d0e0d;
  background-color: rgb(255, 255, 255);
}

div.addNote {
  padding: 10px;
  margin: 10px;
  width: 300px;
  border: 1px solid #0d0e0d;
  background-color: rgb(255, 255, 255);
}

div.delNoteQuest {
  padding: 10px;
  margin: 10px;
  width: 700px;
  border: 1px solid #0d0e0d;
  background-color: rgb(255, 0, 0);
}

button.insButton{
  background-color: #008CBA;
  border: none;
  color: white;
  padding: 5px 30px;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  margin-right: 0;
}


button.clearButton{
  background-color: white;
  border: none;
  color: blue;
  padding: 5px 30px;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  margin-right: 0;
}


button.undoDel{
  background-color: rgb(255, 0, 0);
  border: 1px solid white;
  color: white;
  padding: 5px 30px;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  margin-right: 0;
}


button.delNote{
  background-color: white;
  border: 1px solid white;
  color: rgb(255, 0, 0);
  padding: 5px 30px;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  margin-right: 0;
}


div.container {
  width: 1100px;
  height: 3000px;
  margin: auto;
  border: 1px solid #0d0e0d;
  background-color: rgb(199, 200, 201);
}


</style>