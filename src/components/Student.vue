<template>
	<tr>
		<td>{{ student.id }}</td>
		<td>{{ student.name }}</td>
		<td>{{ student.gender ? "nam" : "nu" }}</td>
		<td>
			<div v-for="(hobby, index) in student.hobbies" :key="index">
				{{ index + 1 }}: {{ hobby }}
			</div>
		</td>
		<td>
			<button
				class="btn danger"
				type="button"
				@click="removeStudent(index)"
			>
				Xoa sinh vien
			</button>
		</td>
	</tr>
</template>

<script>
export default {
	props: ["student", "index", "removeStudent"],
};
</script>
