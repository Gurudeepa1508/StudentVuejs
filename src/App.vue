<template>
  <div id="app">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
     <el-table 
      :data="students"
      style="width: 100%">
      <el-table-column 
        prop="id"
        label="ID"
        width="300">
      </el-table-column>
      <el-table-column 
        prop="name"
        label="Name"
        width="300">
      </el-table-column>
       <el-table-column
        prop="rollnum"
        label="Rollnum"
        width="350">
      </el-table-column>
      <el-table-column
        prop="branch"
        label="Branch"
        width="350">
      </el-table-column>
      <el-table-column
        prop="password"
        label="Password"
        width="350">
      </el-table-column>
      <el-table-column
        prop="delete"
        label="Delete">
         <template slot-scope="scope">
                    <el-button
                      size="mini"
                      type="danger" 
                      icon="el-icon-delete" circle
                         @click="dialogVisible= true;deleteUser(scope.row)"  >
                    </el-button>
                    <el-dialog id="eModal"
                    title="User data is deleted "
                    :visible.sync="dialogVisible" 
                  >
                    <span slot="footer" class="dialog-footer">
                     <el-button type="primary" @click="deleteOk()"> OK</el-button>
                    </span>
                  </el-dialog>
                  </template>       
      </el-table-column>

      <el-table-column
      prop="edit"
      label="Edit">
      <template slot-scope="scope">
        <el-button size="mini" type="primary"  icon="el-icon-edit" circle @click="openDeleteDialog(scope.row)"  >      </el-button>
     
      </template>      
    </el-table-column>
     
    </el-table>
      <el-dialog id="eModal" title="Edit the existing data " :visible.sync="dialogFormVisible"   >
      <el-form :model="form">
        <el-form-item label=" id" :label-width="formLabelWidth">
          <el-input v-model="form.id" disabled autocomplete="off" ></el-input>
        </el-form-item>
        <el-form-item label=" name" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label=" rollnum" :label-width="formLabelWidth">
          <el-input v-model="form.rollnum" autocomplete="off"></el-input>
        </el-form-item>
         <el-form-item label="password" :label-width="formLabelWidth">
          <el-input v-model="form.password" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="branch" :label-width="formLabelWidth">
          <el-select v-model="form.branch" placeholder="Select a branch">
            <el-option label="CSE" value="CSE"></el-option>
            <el-option label="IT" value="IT"></el-option>
            <el-option label="ECE" value="ECE"></el-option>
          </el-select>
        </el-form-item>
       </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="editcancel();dialogFormVisible=false">Cancel</el-button>
          <el-button type="primary" @click="update();dialogFormVisible=false"> update</el-button>
        </span>
      </el-dialog>  
  </div>
</template>
<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from "axios";
export default {  
   data () {
    return {
      dialogVisible:false,
      students:[],
      dialogFormVisible: false,
       form :{
          id:'',
          name: '',
          rollnum: '',
          password:'',
          branch:''
        },
        formLabelWidth: '100px'
      
    }
  },

  name: 'App',
  mounted() {
     axios.get('http://localhost:8088/InsertionChainingWeb/getall')
    .then(response => {   
      this.students=response.data.insertContext;
      
    })
  },
  methods:{
    deleteUser(row){
      console.log(row.id)
      axios.delete('http://localhost:8088/InsertionChainingWeb/delete',{data: {id: row.id.toString() }
})
     
    },  
    openDeleteDialog(row) {
      this.form = row,
      this.form.id=row.id.toString()
      this.dialogFormVisible = true
      console.log('===>', row)
      
},

editcancel(){
  this.dialogVisible = false;
   location.reload();
      
},
deleteOk() {
  this.dialogVisible = false;
  this.selectedRow = null;
  location.reload();
},
update(){
  console.log('update called', this.form)
  axios.post('http://localhost:8088/InsertionChainingWeb/modify',this.form)
  console.log(this.form)
  location.reload();
}
  },
  components: {
    HelloWorld
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>