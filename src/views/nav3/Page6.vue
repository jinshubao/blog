<template>
	<div>
		<el-upload action="https://jsonplaceholder.typicode.com/posts/" list-type="picture-card" multiple="true"
		:on-preview="preview" :on-remove="handleRemove">
			<i class="el-icon-plus"></i>
		</el-upload>
		<el-dialog v-model="dialogVisible" size="tiny">
			<img width="100%" :src="dialogImageUrl" alt="">
		</el-dialog>
	</div>
</template>

<script>
export default {
	data() {
		return {
			dialogImageUrl: '',
			dialogVisible: false
		};
	},
	methods: {
		handleRemove(file, fileList) {
			console.log(file, fileList);
		},
		preview(file) {
			this.dialogImageUrl = file.url;
			this.dialogVisible = true;
		}
	}
}
</script>