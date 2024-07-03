<template>
  <div class="container">
    <form @submit.prevent="handleSubmit" class="form">
      <h1>Form in Vue</h1>
      <div class="field">
        <label>First Name*</label>
        <input
          type="text"
          name="firstName"
          placeholder="Enter First Name"
          v-model="formValues.firstName"
        />
        <p>{{ formErrors.firstName }}</p>
      </div>
      <div class="field">
        <label>Last Name*</label>
        <input
          type="text"
          name="lastName"
          placeholder="Enter Last Name"
          v-model="formValues.lastName"
        />
        <p>{{ formErrors.lastName }}</p>
      </div>
      <div class="field">
        <label>Email*</label>
        <input
          type="text"
          name="email"
          placeholder="Enter email"
          v-model="formValues.email"
        />
        <p>{{ formErrors.email }}</p>
      </div>
      <div class="field">
        <label>Contact*</label>
        <input
          type="text"
          name="contact"
          placeholder="Enter Mobile number"
          v-model="formValues.contact"
        />
        <p>{{ formErrors.contact }}</p>
      </div>
      <div class="field">
        <label>Gender*</label>
        <div class="radio-group">
          <input
            type="radio"
            id="male"
            value="Male"
            v-model="formValues.gender"
          />
          <label for="male">Male</label>
          <input
            type="radio"
            id="female"
            value="Female"
            v-model="formValues.gender"
          />
          <label for="female">Female</label>
          <input
            type="radio"
            id="other"
            value="Other"
            v-model="formValues.gender"
          />
          <label for="other">Other</label>
        </div>
        <p>{{ formErrors.gender }}</p>
      </div>
      <div class="field">
        <label>Your Best Subject</label>
        <div class="checkbox-group">
          <input
            type="checkbox"
            id="english"
            value="English"
            v-model="formValues.subjects"
          />
          <label for="english">English</label>
          <input
            type="checkbox"
            id="maths"
            value="Maths"
            v-model="formValues.subjects"
          />
          <label for="maths">Maths</label>
          <input
            type="checkbox"
            id="physics"
            value="Physics"
            v-model="formValues.subjects"
          />
          <label for="physics">Physics</label>
        </div>
      </div>
      <div class="field">
        <label>Upload Resume*</label>
        <input
          type="file"
          @change="handleFileUpload"
        />
        <p>{{ formErrors.resume }}</p>
      </div>
      <div class="field">
        <label>URL*</label>
        <input
          type="text"
          name="url"
          placeholder="Enter URL"
          v-model="formValues.url"
        />
        <p>{{ formErrors.url }}</p>
      </div>
      <div class="field">
        <label>Select your choice</label>
        <select v-model="formValues.choice">
          <option disabled value="">Select your Ans</option>
          <option>HTML</option>
          <option>CSS</option>
          <option>JavaScript</option>
        </select>
      </div>
      <div class="field">
        <label>About</label>
        <textarea
          name="about"
          placeholder="About yourself"
          v-model="formValues.about"
        ></textarea>
      </div>
      <div class="buttons">
        <button type="reset" @click="handleReset">Reset</button>
        <button type="submit">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formValues: {
        firstName: "",
        lastName: "",
        email: "",
        contact: "",
        gender: "",
        subjects: [],
        resume: null,
        url: "",
        choice: "",
        about: "",
      },
      formErrors: {},
      isSubmit: false,
    };
  },
  methods: {
    handleFileUpload(event) {
      this.formValues.resume = event.target.files[0];
    },
    handleReset() {
      this.formValues = {
        firstName: "",
        lastName: "",
        email: "",
        contact: "",
        gender: "",
        subjects: [],
        resume: null,
        url: "",
        choice: "",
        about: "",
      };
      this.formErrors = {};
      this.isSubmit = false;
    },
    handleSubmit() {
      this.formErrors = this.validate(this.formValues);
      this.isSubmit = true;
      if (Object.keys(this.formErrors).length === 0) {
        console.log("Form submitted successfully:", this.formValues);
      }
    },
    validate(values) {
      const errors = {};
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/i;
      const urlRegex = /^(ftp|http|https):\/\/[^ "]+$/;
      if (!values.firstName) {
        errors.firstName = "First Name is required!";
      }
      if (!values.lastName) {
        errors.lastName = "Last Name is required!";
      }
      if (!values.email) {
        errors.email = "Email is required!";
      } else if (!emailRegex.test(values.email)) {
        errors.email = "This is not a valid email format!";
      }
      if (!values.contact) {
        errors.contact = "Contact is required!";
      } else if (isNaN(values.contact)) {
        errors.contact = "Contact must be a valid number!";
      }
      if (!values.gender) {
        errors.gender = "Gender is required!";
      }
      if (!values.resume) {
        errors.resume = "Resume is required!";
      }
      if (!values.url) {
        errors.url = "URL is required!";
      } else if (!urlRegex.test(values.url)) {
        errors.url = "This is not a valid URL format!";
      }
      return errors;
    },
  },
};
</script>

<style scoped>
body {
  font-family: 'Helvetica Neue', Arial, sans-serif;
  background-color: #eef2f7;
  display: flex;
  justify-content: center;
  align-items: flex-start; 
  height: 100vh;
  margin: 0;
  padding: 10px; 
  overflow-y: auto; 
} 

.container {
  max-width: 600px;
  width: 100%;
  height: 100vh;
} 

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 20px;
}

 .form {
display: flex;
flex-direction: column;
background-color: #fff;
  padding: 30px 50px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);


}

.field {
  margin-bottom: 10px;
 
} 

.field label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
  color: #555;
}

.field input[type="text"],
.field input[type="file"],
.field textarea,
.field select {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  transition: border-color 0.3s;
}

.field input[type="text"]:focus,
.field input[type="file"]:focus,
.field textarea:focus,
.field select:focus {
  border-color: #66afe9;
  outline: none;
}

.field input[type="radio"],
.field input[type="checkbox"] {
  margin-right: 8px;
}

.radio-group,
.checkbox-group {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.field p {
  color: red;
  font-size: 12px;
  margin-top: 5px;
}

.buttons {
  display: flex;
  justify-content: space-between;
}

.buttons button {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

.buttons button[type="reset"] {
  background-color: #ff4d4d;
  color: white;
}

.buttons button[type="submit"] {
  background-color: #28a745;
  color: white;
}

.buttons button[type="reset"]:hover {
  background-color: #ff1a1a;
}

.buttons button[type="submit"]:hover {
  background-color: #218838;
}
</style>
