<template>
  <div>
    <div class="wrapper">
    </div>
    <div class="container">


      <h1>CREATE A PROJECT</h1>

      <sui-form @submit.prevent="handleSubmit">


        <sui-form-field v-if="isAdmin">
          <h3>Business Contact</h3>
          <input
             type="text"
             placeholder="Enter business ID"
             v-model="newProject.project_owner_id">
        </sui-form-field>

        <sui-form-field>
          <h3>Project Title</h3>
          <p>Should be a short, descriptive summary of the project.</p>
          <input
             type="text"
             placeholder="Ex. Sales dashboard, Insurance marketplace, Health tracker"
             v-model="newProject.project_name">
        </sui-form-field>

        <sui-form-field>
          <h3>Role Type</h3>
          <p>Is this project for a web developer or data scientist?</p>
          <sui-dropdown
            placeholder="Full Stack Web Developer"
            selection
            :options="roles"
            v-model="newProject.role_type"
          />
        </sui-form-field>

        <sui-form-field>
          <h3>Project type</h3>
          <p>Is this a capstone project or another type of opportunity?</p>
          <sui-dropdown
            selection
            value="project_type"
            :options="project_types"
            v-model="newProject.project_type"
          />
        </sui-form-field>

        <sui-form-field>
          <h3>Tools</h3>
          <p>What tools or technologies should the student use? (optional)</p>
          <input
            type="text"
            placeholder="Ex. JavaScript, React, Android, iOS, Python, Java, etc."
            v-model="newProject.tools">
        </sui-form-field>

        <sui-form-field>
          <h3>Description</h3>
          <p>Describe the scope and main features of this project.</p>
          <input
            type="text"
            class="tall"
            v-model="newProject.description">
        </sui-form-field>

        <sui-form-field>
          <h3>Business Problem</h3>
          <p>What business problem does this project solve? This helps the student understand the context and purpose of the project.</p>
          <input
            type="text"
            class="medium"
            v-model="newProject.business_problem">
        </sui-form-field>



        <sui-form-field>
          <h3>Is there an opportunity for the student to get paid for this project?</h3>
          <sui-dropdown
            placeholder="No/Not applicable for capstone projects"
            selection
            :options="payment_options"
            v-model="newProject.paid_opportunities"
          />
        </sui-form-field>


        <sui-button type="submit" color="orange">
            Submit
        </sui-button>
      </sui-form>



  </div>
</div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';

export default {
  name: "Project",
  computed: {...mapGetters([
    'isLoggedIn',
    'getCurrentProject',
    'isAdmin',
    'isStudent',
    'getBusinesses',
  ]) },
  methods: {
    ...mapActions(['addNewProject', 'fetchAllOpenProjects']),
    handleSubmit: function(){
      // this.addNewProject()
      this.addNewProject(this.newProject);
      this.fetchAllOpenProjects();
    }
  },
  data() {
    return {
      newProject:
      {
               "project_owner_id": null,
               "committed_student_id": null,
               "project_name": "Short and descriptive title",
               "project_type": "Capstone",
               "tools": "Javascript",
               "paid_opportunities": "this is a capstone project",
               "role_type": "Web Developer",
               "description": "",
               "business_problem": ""
      },
      project_types: [
        { key : 'capstone', text: "Capstone", value: "capstone"},
        { key: "consulting", text: 'Consulting', value: "consulting"},
        { key: "internship", text: 'Internship', value: "internship"},
        { key: "postgrad", text: 'Post-Graduation Project', value: "postgrad"}
      ],
      roles: [
        { key : 'All', text: "All", value: "All"},
        { key: "webdev", text: 'Full Stack Web Developer', value: "Full Stack Web Developer"},
        { key: "datascience", text: 'Data Scientist', value: "Data Scientist"}
      ],
      payment_options: [
        { key : "No", text: "No/Not applicable for capstone projects", value: "No"},
        { key : "Yes", text: "Yes", value: "Yes"}
      ]
    };
  }
};
</script>

<style scoped>

h1 {
  font-family: "museo-sans", sans-serif;
  color: white;
  letter-spacing: .4rem;
  font-weight: 200;
  margin-top: 20px;
  margin-bottom: 10px;
}

h3 {
  margin-top: 30px;
  color: orange;
}

h4 {
  margin-top: 0;
  color: gray;
}

.tall {
  height: 200px;
}

.medium {
  height: 150px;
}

.container{
  margin-top: 60px;
  margin-left: 20%;
  margin-right: 20%;
}


.wrapper {
	height: 110px;
	width: 100%;
	background-image: url('../img/gerome-bruneau-65759-unsplash.jpg');
	position: absolute;
	left: 0;
	top: 60px;
	display: block;
	align-items: left;
  padding-top: 50px;
  padding-left: 20%;
  padding-right: 20%;
  z-index: -1;
}

</style>
