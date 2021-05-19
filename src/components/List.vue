<template>
	<div class="container">
		<div class="title">Add Student</div>
		<form class="add-student">
			<div class="form-group">
				<label for="id">MSSV</label>
				<input type="number" id="id" v-model="student.id" />
			</div>
			<div class="form-group">
				<label for="name">Ho va Ten</label>
				<input type="text" id="name" v-model="student.name" />
			</div>
			<div class="form-group">
				<label for="gender">Gioi tinh</label>
				<select id="gender" v-model="student.gender">
					<option value="0">Vui long chon gioi tinh</option>
					<option value="1">Nam</option>
					<option value="2">Nu</option>
				</select>
			</div>
			<div
				class="form-group"
				v-for="(hobby, index) in hobbies"
				:key="index"
			>
				<label for="hobby">So thich {{ index + 1 }}</label>
				<input
					type="text"
					id="hobby"
					v-model="student.hobbies[index]"
				/>
				<button
					class="btn"
					type="button"
					v-if="!index"
					@click="hobbies.push(1)"
				>
					Them so thich
				</button>
				<button
					class="btn danger"
					type="button"
					v-if="index"
					@click="
						hobbies.splice(index, 1);
						student.hobbies.splice(index);
					"
				>
					Xoa
				</button>
			</div>
			<div class="form-group">
				<button class="btn" type="button" @click="addStudent">
					Them sinh vien
				</button>
			</div>
		</form>
		<table>
			<tr>
				<th>MSSV</th>
				<th>Ho va Ten</th>
				<th>Gioi tinh</th>
				<th>So thich</th>
				<th></th>
			</tr>
			<student
				v-for="(student, index) in students"
				:key="index"
				:student="student"
				:index="index"
				:removeStudent="removeStudent"
			/>
		</table>
	</div>
</template>

<script>
import Student from "./Student.vue";
export default {
	data() {
		return {
			hobbies: [1],
			student: {
				hobbies: [],
				gender: 0,
			},
			students: [
				{
					id: 1,
					name: "Nguyen Van A",
					gender: 1,
					hobby: [],
				},
				{
					id: 2,
					name: "Nguyen Thi B",
					gender: 0,
					hobby: [],
				},
			],
		};
	},
	methods: {
		isValid() {
			return this.student.name && this.student.id && this.student.gender;
		},
		addStudent() {
			if (this.isValid()) {
				this.students.push(this.student);
				this.resetForm();
			} else {
				alert("vui long nhap thong tin sinh vien!");
			}
		},
		removeStudent(index) {
			this.students.splice(index, 1);
		},
		resetForm() {
			this.student = {
				hobbies: [],
				gender: 0,
			};
		},
	},
	components: {
		Student,
	},
};
</script>

<style>
* {
	font-family: arial, sans-serif;
}
.container {
	max-width: 1140px;
	height: 100vh;
	margin: 5rem;
}
.title {
	font-weight: 600;
	font-size: 20px;
	text-transform: uppercase;
	text-align: center;
}
.form-group {
	width: 100%;
	display: flex;
	flex-wrap: wrap;
	margin: 1.5rem 0.5rem;
}
.form-group label {
	width: 15%;
}
table {
	border-collapse: collapse;
	width: 100%;
}
td,
th {
	border: 1px solid #dddddd;
	text-align: left;
	padding: 8px;
	text-align: center;
}

tr:nth-child(even) {
	background-color: #dddddd;
}
.btn {
	background-color: #008CBA; /* Green */
	border: none;
	color: white;
	padding: 10px 15px;
	text-align: center;
	text-decoration: none;
	display: inline-block;
	font-size: 16px;
	cursor: pointer;
	border-radius: 5px;
}
.btn.danger {
	background-color: #f44336;
}
</style>
