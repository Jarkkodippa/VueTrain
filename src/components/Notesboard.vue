<template>
  <div class="container">
    
    <form>

    <table class="totTable">
      <thead>
        <tr>
          <th>Total</th>
          <th>Completed</th>
          <th>Not completed</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{{ sortedNotes.length }}</td>
          <td>{{ this.completed }}</td>
          <td>{{ this.NCompleted }}</td>
        </tr>
      </tbody>
    </table>

    <div class="resultDiv">
    <table class="resultTable">
      <thead style="background: gray; color: white;">
        <tr>
          <th @click="sort('id')">Id</th>
          <th @click="sort('title')">Title</th>
          <th @click="sort('content')">Content</th>
          <th @click="sort('status')">Status</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(fieldVal, i) in sortedNotes" :key="i">
          <td><input type="checkbox" v-model="fieldVal.DelNotes" @click="DelQuestion()">{{ fieldVal.id }}</td>
          <td>{{ fieldVal.title }}</td>
          <td>{{ fieldVal.content }}</td>
          <td>{{ fieldVal.status }}</td>
        </tr>
      </tbody>
    </table>

    <div style="display:flex; justify-content:flex-end; width:100%; padding:0;">
    <button type="button" @click="onAdd" class="insButton" id="onAdd">
        Add
      </button>
    </div>
    </div>

    <div v-show="hideForm" class="addNote">
    <h1 class="noteHeader">Add Note</h1>
    
      <div class="form-group">
        <input
          type="text"
          placeholder="Add note"
          v-model="title"
          class="form-control"
          id="title"
        />
        <br>
        <input
          type="text"
          placeholder="Lorem ipsum"
          v-model="content"
          class="form-control"
          id="content"
        />
        <br>

        <input
          type="text"
          placeholder="New"
          v-model="status"
          class="form-control"
          id="status"
        />

      
      </div>
      <button type="button" @click="SubmitNote" class="insButton" id="Save" >
        Save
      </button>

      <button type="button" @click="clearForm" class="clearButton" id="clearButton">
        Cancel
      </button>
    
    </div>

  <div v-show="hideDelFormDiv" class="delNoteQuest">
  <h1>Do you want to delete this note?

  <button type="button" @click="HideDelForm" class="undoDel" id="undoDel" >
    No
  </button>

  <button type="button" @click="DelNote" class="delNote" id="delNote">
    Yes
  </button>
  </h1>

  </div>
  

  </form>

  </div>
</template>

<script>

import json from './importexample.json'

export default {
  name: "NotesBoard",
  data: () => ({ hideForm: false, currentSort:'title',currentSortDir:'asc', 
                  id: 0, title: "", content: "", status: "", notesTbl: [], 
                  hideDelFormDiv: false, completed:0, NCompleted:0, jsonData:json.data }),
  
  created:function(){
    for(var h in this.jsonData)
    {
      this.notesTbl.push({ id: this.jsonData[h].id, title: this.jsonData[h].title, 
                            status: this.jsonData[h].status, 
                            content: this.jsonData[h].content, DelNotes: false });
      this.id = this.jsonData[h].id;
    }
  },
  
  computed: {
    sortedNotes: function() {
    return this.notesTbl.slice().sort((a,b) => {
      let modifier = 1;
      if(this.currentSortDir === 'desc') modifier = -1;
      if(a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
      if(a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
      return 0;
    });
    },
  },

  methods: {
    sort:function(s) {
      if(s === this.currentSort) {
        this.currentSortDir = this.currentSortDir==='asc'?'desc':'asc';
      }
      this.currentSort = s;
    },
    SubmitNote() {
      if(this.title == "" && this.content == "")
      {
        alert("both fields shouldn’t be empty");
        return false;
      }

      if(this.status == "Completed")
        this.completed++;
      else
        this.NCompleted++;

      this.id++;
      this.notesTbl.push({ id: this.id, title: this.title, status: this.status, 
                            content: this.content, DelNotes: false });
      this.clearForm();
    },
    onAdd() {
      this.hideForm = true;
    },
    DelQuestion() {
      this.hideDelFormDiv = true;
    },
    clearForm() {
      this.title = "";
      this.content = "";
      this.status = "";
      this.hideForm = false;
    },
    HideDelForm() {
      for(var k in this.notesTbl)
      {
        this.notesTbl[k].DelNotes = false;
      }
      this.hideDelFormDiv = false;
    },
    DelNote(){
      for(var k in this.notesTbl)
      {
        
        if(this.notesTbl[k].DelNotes == true)
        {
          
          if(this.notesTbl[k].status == "Completed")
            this.completed--;
          else
            this.NCompleted--;
          
          this.notesTbl.splice(k,1);
        }
      }

      this.HideDelForm();
    }
  },
};
</script>