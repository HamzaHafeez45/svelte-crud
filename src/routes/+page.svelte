<script>
	let schoolName = "";
	let editRowIndex = -1;

	let allSchools = [
		{
			schoolName: "school 1"
		},
		{
			schoolName: "school 2"
		}
	];

	const submitForm = () => {
		if (editRowIndex > -1) {
			allSchools[editRowIndex] = { schoolName };
		} else {
			allSchools.push({ schoolName });
		}

		allSchools = allSchools;
		schoolName = "";
		editRowIndex = -1;
	};

	const editSchool = (index) => {
		editRowIndex = index;
		schoolName = allSchools[editRowIndex].schoolName;
	};

	const deleteSchool = (index) => {
		allSchools.splice(index, 1);
		allSchools = allSchools;
	};
</script>

<div id="header"><h1>CRUD OPERATIONS</h1></div>

<div id="form-section">
	<form on:submit|preventDefault={submitForm}>
		<label for="schoolName">School Name</label>
		<input
			type="text"
			placeholder="Enter Name of School"
			name="schoolName"
			required
			bind:value={schoolName}
		/>

		<br /><br />
		<input type="submit" value={editRowIndex > -1 ? 'Edit School' : 'Add School'} />
	</form>
</div>
<hr />
<table id="schools">
	<thead>
		<tr>
			<th>#</th>
			<th>School Name</th>
			<th>Actions</th>
		</tr>
	</thead>
	<tbody>
		{#each allSchools as school, index (index)}
			<tr>
				<td>{index + 1}</td>
				<td>{school.schoolName}</td>
				<td>
					<button on:click={() => editSchool(index)}>Edit</button>
					<button on:click={() => deleteSchool(index)}>Delete</button>
				</td>
			</tr>
		{/each}
	</tbody>
</table>

<style>
	:global(body) {
		margin: auto;
		width: 80%;
		padding: 10px;
	}
	#header {
		text-align: center;
		padding-top: 30px;
		padding-bottom: 30px;
		margin-bottom: 30px;
		color: inherit;
		background-color: #eee;
	}
	input[type='text'] {
		width: 100%;
		padding: 12px 20px;
		margin: 8px 0;
		display: inline-block;
		border: 1px solid #ccc;
		border-radius: 4px;
		box-sizing: border-box;
	}
	input[type='submit'] {
        width: 100%;
		border: 0;
		cursor: pointer;
		border-radius: 6px;
		padding: 14px 20px;
		font-weight: bold;
		color: black;
		background: white;
		border: 2px solid black;
	}
	#schools {
		border-collapse: collapse;
		width: 100%;
	}

	#schools td,
	#schools th {
		border: 1px solid #ddd;
		padding: 8px;
	}

	#schools tr:nth-child(even) {
		background-color: #f2f2f2;
	}

	#schools tr:hover {
		background-color: #ddd;
	}

	#schools th {
		padding-top: 12px;
		padding-bottom: 12px;
		text-align: left;
		background-color: black;
		color: white;
	}
	button {
		border: 0;
		cursor: pointer;
		border-radius: 6px;
		padding: 8px 12px;
		font-weight: bold;
		color: black;
		background: white;
		border: 2px solid black;
	}
</style>
