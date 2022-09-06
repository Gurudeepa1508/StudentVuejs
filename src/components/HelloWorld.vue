<template>
  <div class="hello">
<el-button type="primary" @click="dialogFormVisible= true">Create a new account</el-button>
<el-dialog title="Register" :visible.sync="dialogFormVisible">
  <el-form :model="form">
    <el-form-item label=" name" :label-width="formLabelWidth">
      <el-input v-model="form.name" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label=" rollnum" :label-width="formLabelWidth">
      <el-input v-model="form.rollnum" autocomplete="off"></el-input>
    </el-form-item>
     <el-form-item label=" password" :label-width="formLabelWidth">
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
    <el-button @click="dialogFormVisible = false">Cancel</el-button>
    <el-button type="primary" @click="dialogForm();dialogFormVisible = false">Confirm</el-button>
  </span>
 </el-dialog>
  </div>      
</template>

<script>
import axios from "axios";
export default {
  // name: 'HelloWorld',
  // props: {
  //   msg: String
  // }
    
   data() {
        return { 
   
       dialogFormVisible: false,
       form: {
          name: '',
          rollnum: '',
          password:'',
          branch:''
        },
        formLabelWidth: '100px'
      
           }
      },
      methods: {
        dialogForm(){
          console.log(this.form)
            axios.post('http://localhost:8088/InsertionChainingWeb/insert', this.form)
            location.reload();
                 
                },
      },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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

