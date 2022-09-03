<template>
  <div id="app">
	  <div class="homeHeader">用户管理</div>
	  
	
		  
		  
<div style="width: 70%; margin-left: 600px;">
	<div style="margin-top: 30px;">
		   <el-button type="primary" icon="el-icon-plus" @click="showAddUserView">新建</el-button>
		 <el-input
	            style="width: 300px; margin-left:20px"
	            prefix-icon="el-icon-search"
	            v-model="empName"
	            @keydown.enter.native="initEmps"
	            clearable
	            @clear="initEmps"
	            :disabled="showAdvanceSearchVisible"
	            placeholder="请输入员工名进行搜索..."
	          ></el-input>
	          <el-button
			  style=" margin-left:20px"
	            type="primary"
	            icon="el-icon-search"
	            @click="initEmps"
	            :disabled="showAdvanceSearchVisible"
	            >搜索</el-button
	          >
	     <el-button
		 style=" margin-left:280px"
	       type="primary"
	       @click="initEmps"
	       :disabled="showAdvanceSearchVisible"
	       >撤销</el-button
	     >
	</div>
	 <el-table 
	        :data="userList"
			border
			style="width: 870px;margin-top: 20px;">
	        <el-table-column type="selection" width="55"></el-table-column>
	        <el-table-column prop="name" label="姓名" fixed width="90" align="left">
	        </el-table-column>
	        <el-table-column prop="age" label="年龄" width="85" align="left">
	        </el-table-column>
	        <el-table-column
	          prop="gender"
	          label="性别"
	          width="50"
	        ></el-table-column>
	       
	        <el-table-column
	          prop="phone"
	          label="联系电话"
	          align="left"
	          width="100"
	        ></el-table-column>
	        <el-table-column
	          prop="address"
	          label="详细地址"
	          align="left"
	          width="270"
	        ></el-table-column>
	        <el-table-column label="操作"  width="200">
	          <template slot-scope="scope">
	            <el-button
	           @click="showEditUserView(scope.row)"
	              style="padding: 3px"
	              size="mini"
	              >编辑</el-button>
	            <el-button
	          
	              style="padding: 3px"
	              size="mini"
	              type="danger"
	              @click="deleteRow(scope.$index, userList)">删除</el-button
	            >
	          </template>
	        </el-table-column>
	      </el-table>


</div> 

	
	 <el-dialog :title="title" :visible.sync="dialogVisible" width="50%">
		 <div>
			<el-form label-position="top" ref="userForm" :model="user">
					<el-row>
			              <el-col :span="6">
						  <el-form-item label="姓名" prop="name">
			                <el-input
			                  size="mini"
			                  prefix-icon="el-icon-edit"
			                  style="width: 150px"
			                  v-model="user.name"
			                  placeholder="请输入员工姓名"
			                ></el-input>
			              </el-form-item>
			              </el-col>
						  <el-col :span="6">
						  <el-form-item label="性别">
						                 <el-select
						                   v-model="user.gender"
						                   size="mini"
						                   style="width: 200px"         >
						                 <el-option label="男" value="男"></el-option>
						                       <el-option label="女" value="女"></el-option>
						                 </el-select>
						               </el-form-item>
						  </el-col>
					</el-row>
			         
					 <el-row>
					    <el-col :span="6">
					 	  <el-form-item label="联系电话" prop="name">
					         <el-input
					           size="mini"
					           prefix-icon="el-icon-edit"
					           style="width: 150px"
					           v-model="user.phone"></el-input>
					       </el-form-item>
					       </el-col>
					 </el-row>
					 
					 <el-row>
					    <el-col :span="6">
					 	  <el-form-item label="联系地址" prop="name">
					         <el-input
					           size="mini"
					           prefix-icon="el-icon-edit"
					           style="width: 150px"
					           v-model="user.address"></el-input>
					       </el-form-item>
					       </el-col>
					 </el-row>
			</el-form> 
			
		 </div>
		    <span slot="footer" class="dialog-footer">
		         <el-button @click="dialogVisible = false">取 消</el-button>
				   <el-button v-show="showAdd" type="primary" @click="add">添加</el-button>
		         <el-button v-show="showUpdate" type="primary" @click="alter">修改</el-button>
		       </span>
	 </el-dialog>
	  
 <!--   <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
	<el-button type="info">测试element-ui是否成功导入</el-button> -->
  </div>
</template>

<script>


export default {
  name: 'app',
  data(){
	  return {
		  userList:[
			  {		id:1,
				  name:"黄寿祥",
				  age: 22,
				  gender:'男',
				  phone:'15791397049',
				  address:'广州软件学院'
			  },  {
				  id:2,
				  name:"黄寿祥",
				  age: 22,
				  gender:'男',
				  phone:'15791397049',
				  address:'广州软件学院'
			  },  {
				  id:3,
				  name:"黄寿祥",
				  age: 22,
				  gender:'男',
				  phone:'15791397049',
				  address:'广州软件学院'
			  }
		  ],
		  user:{
			  id:null,
			  name:'',
			  age: null,
			  gender:'',
			  phone:'',
			  address:''
		  },
		title:'',
		showAdd:false,
		showUpdate:false,
		dialogVisible:false	  
	  }
  },
  methods:{
	  showAddUserView(){
		this.user = {
			id:null,
			name:'',
			age: null,
			gender:'',
			phone:'',
			address:''
		}; 
		 this.title = "新建用户",
		 this.dialogVisible = true;
		this.showAdd = true;
		this.showUpdate = false;
	  },
	  showEditUserView(data){
		
		  this.title = "编辑用户";
		  this.showAdd = false;
		  this.showUpdate = true;
		  this.user = data;
		  console.log(this.user);
		  this.dialogVisible = true;  
	  },
	  add(){
		this.user.id = this.userList.length+1;
	    this.userList.push(this.user);
	    this.dialogVisible = false ;
		this.showAdd=false;
		this.showUpdate=false;
	  },
	  alter(){
	      this.dialogVisible = false;
	      this.showAdd=false;
	      this.showUpdate=false;
	  
	  },
	  deleteRow(index, rows) {
	      rows.splice(index, 1);
	  }
  }

}
</script>

<style>
.homeHeader {
  background: #409eff;
  height: 100px;
  align-items: center;
  justify-content: space-between;
  padding: 0 15px;
  box-sizing: border-box;
   /*!*居中*!*/
    text-align: center;
	 line-height: 100px;
    /*字体大小*/
    font-size: 30px;
    /*字体*/
    font-family: 华文楷体;
}
</style>
