<template>
	<div class="home">
	<el-button
          size="mini"
          @click="handleEdit">添加</el-button>
<div v-show='ww'>
          	<input type="text" placeholder="姓名" v-model="aa.name">
          	<input type="text" placeholder="性别" v-model="aa.sex">
          	<input type="text" placeholder="state" v-model="aa.state">
          	
          </div>

			<el-table :data="tableData" style="width: 100%">
				<el-table-column prop="id" label="学号" width="180">
				</el-table-column>
				<el-table-column prop="name" label="姓名" width="180">
				</el-table-column>
				<el-table-column prop="sex" label="性别">
				</el-table-column>
				 <el-table-column label="操作">
      <template slot-scope="scope">
        
          
		
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.row)">删除</el-button>
      </template>
    </el-table-column>
			</el-table>
	</div>
</template>

<script>
	export default {
	data() {
			return {
				tableData:[],
				aa:{},
				ww:false
				
			}
		},
	     watch:{
	      '$route':function(){
	     	 this.$http.post('http://localhost:3000',{state:this.$route.params.id},{emulateJSON:true}).then(e=>this.tableData=e.body)
	      }
	     },
		created(){
			this.$http.post('http://localhost:3000',{state:this.$route.params.id},{emulateJSON:true}).then(e=>this.tableData=e.body)
		},
		methods:{
			handleDelete(row){
			console.log(row)
			   this.$http.post('http://localhost:3000/del',{id:row.id},{emulateJSON:true}).then(e=>this.row=e.body)
			   this.$http.post('http://localhost:3000',{state:this.$route.params.id},{emulateJSON:true}).then(e=>this.tableData=e.body)
			   
			},
			handleEdit(){
			 this.$http.post('http://localhost:3000/add',this.aa,{emulateJSON:true}).then(()=>{})
			 this.ww=!this.ww
			}

			 
		}
	}
</script>
