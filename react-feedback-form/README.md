# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh



What you will learn
In this lab, you will create a feedback form using React functional components and manage user details using the useState hook. You will implement event handlers to manage form input changes, validate user inputs, and handle form submissions. Additionally, you will create a confirmation dialog using the confirm method to confirm user details before final submission. Upon successful submission, you will reset the form fields and display a thank you message to the user. This lab will give you practical experience building interactive forms and handling user inputs in React applications.
Learning objectives
After completing this lab, you will be able to:
•	Create a form to collect user feedback, including their name, email, and the feedback message.
•	Handle form submission, including data validation, to ensure that the users enter their names and provide feedback before submitting the form.
•	Display a confirmation dialog to users after they submit their feedback, showing the information they entered and prompting them to confirm before final submission.
•	Reset the form fields to clear the input values and provide users with a clean form for submitting additional feedback.
Prerequisites
•	Basic knowledge of HTML
•	Intermediate knowledge of JavaScript
•	Basic knowledge of React function component, useState hook, and handling forms
Setting up the environment
1.	From the menu on top of the lab, click the Terminal tab at the top-right of the window shown at number 1 in the given screenshot, and then click New Terminal as shown at number 2.
 
2.	Write the following command in the terminal and hit Enter to clone the boiler template for this React application.
1.	1
1.	git clone https://github.com/ibm-developer-skills-network/feedback_form.git
Copied!
3.	This will create a folder named feedback_form under the project folder name, and the structure will be as shown in the given screenshot. The feedback_form application includes a class component named FeedbackForm.jsx and a css file named FeedbackForm.css.
 
4.	Write the command to enter the feedback_form folder in the terminal. The command will set your terminal path to run the React application in the feedback_form folder.
1.	1
ii.	cd feedback_form
Copied!
5.	To make sure that the code you have cloned is working correctly, you need to follow the given steps:
o	Write the following command in the terminal and select Enter to install all the necessary packages to execute the application.
1.	1
b.	npm install
Copied!
o	Then execute the following command to run the application, providing you with port number 4173.
1.	1
b.	npm run preview
Copied!
6.	To view your React application, click the Skills Network icon on the left panel (refer to number 1). This action will open the Skills Network Toolbox. Next, click Launch Application (refer to number 2). Enter port number 4173 in Application Port (refer to number 3) and click  .
 
7.	The output will display as shown in the given screenshot.
 
8.	You can preserve your latest work on this lab by adding, committing, and pushing it to your GitHub repository. This ensures that even if you’re not working on the task continuously, your progress will be saved, allowing you to resume from where you left off.
Note: Step 8 is optional.


Step 3: Create basic template
1.	Navigate to the Components folder in your React project's src folder.
2.	Navigate to the FeedbackForm.jsx component located within the src folder of your React project. Inside the return of this component, you have a <nav> tag and a <form> tag with class name feedback-form, which includes a child <h2> tag with a <p> tag.
3.	To create the feedback form, you need to include three input fields and create one button to handle the user's following details.
o	First input box for username
o	Second input box for user email ID
o	Third input box for user feedback

xix.	<input
xx.	          type="text"
xxi.	          name="name"
xxii.	          placeholder="Your Name"
xxiii.	        />
xxiv.	        <input
xxv.	          type="email"
xxvi.	          name="email"
xxvii.	          placeholder="Your Email"
xxviii.	        />
xxix.	        <textarea
xxx.	          name="feedback"
xxxi.	          placeholder="Your Feedback"
xxxii.	        ></textarea>
xxxiii.	        <button type="submit">Submit Feedback</button>
Copied!
4.	To see the latest output, perform ctrl+c and re-run the application in the terminal. You will see the output in the screenshot.
 
Note: If application is already running then you just need to refresh the application page

Step 4: Initialize states to handle form data
1.	Integrate the useState hook from React at the top of the component to manage the form data state. Use the useState hook to create state variables for the form data details such as name, email, and feedback.
1.	1
ii.	import React, { useState } from 'react';
Copied!
2.	Initialize the details with empty strings.You need to initialize an object, including name, email, and feedback form details, using the useState hook.

vi.	const [formData, setFormData] = useState({
vii.	    name: '',
viii.	    email: '',
ix.	    feedback: ''
x.	  });
Copied!
Note: Include the above code before return of this component.


Step 5: Implement change handlers
1.	Define a handleChange function to update the form data state as users input their information. Create this after you have initialized variables with useState hook.
2.	Inside the handleChange function, extract the name and value of the input field from the event object.
3.	Update the form data state using the setFormData function and spread operator to merge the new value with the existing form data.

viii.	 const handleChange = (event) => {
ix.	  const { name, value } = event.target;
x.	  setFormData({
xi.	    ...formData,
xii.	    [name]: value
xiii.	  });
xiv.	};
Copied!
•	const handleChange = (event) => { ... }: This line declares a constant named handleChange and assigns it an arrow function. The function takes an event parameter, representing the event triggered by the user's interaction with an input element.
•	const { name, value } = event.target;: This line extracts the name and value properties from the event object's target property. The target property refers to the DOM element that triggered the event, which, in this case, is an input field. The name property corresponds to the 'name' attribute of the input field, while the value property represents the current 'value' entered by the user into the input field.
•	setFormData({ ...formData, [name]: value });: The setFormData function is a state updater function provided by React's useState hook to update the state variable formData. It spreads the existing formData object and then updates the property specified by the 'name' variable with the new value. This pattern ensures that the state is updated immutably, meaning a new object is created with the updated property rather than modifying the existing state directly.
Step 6: Integrate form state and onchange event
1.	In the JSX code, bind the form input fields, name, email, and feedback to their respective state variables using formData.name, formData.email, and formData.feedback.
2.	Use the value attribute to set the input field values and the onChange attribute to call the handleChange function when the input values change.

xxi.	<input
xxii.	          type="text"
xxiii.	          name="name"
xxiv.	          placeholder="Your Name"
xxv.	          value={formData.name}
xxvi.	          onChange={handleChange}
xxvii.	        />
xxviii.	        <input
xxix.	          type="email"
xxx.	          name="email"
xxxi.	          placeholder="Your Email"
xxxii.	          value={formData.email}
xxxiii.	          onChange={handleChange}
xxxiv.	        />
xxxv.	        <textarea
xxxvi.	          name="feedback"
xxxvii.	          placeholder="Your Feedback"
xxxviii.	          value={formData.feedback}
xxxix.	          onChange={handleChange}
xl.	        ></textarea>
Copied!
Note: Include value and onchange attributes in your previous input field and text area.

Step 7: Handle form submission
1.	Implement the form submission functionality by defining a handleSubmit function. This function should take an event parameter and prevent the default form submission.
2.	Then, create a variable named confirmationMessage to capture user details.
3.	Next, create another variable, isConfirmed, to confirm whether the user's details are correct.
4.	If confirmed, log the form data to the console, display a thank you message to the user using the alert box, and clear the form fields by resetting the form data state.

xix.	const handleSubmit = (event) => {
xx.	    event.preventDefault();
xxi.	    const confirmationMessage = `
xxii.	      Name: ${formData.name}
xxiii.	      Email: ${formData.email}
xxiv.	      Feedback: ${formData.feedback}
xxv.	    `;
xxvi.	    const isConfirmed = window.confirm(`Please confirm your details:\n\n${confirmationMessage}`);
xxvii.	    if (isConfirmed) {
xxviii.	      console.log('Submitting feedback:', formData);
xxix.	      setFormData({
xxx.	        name: '',
xxxi.	        email: '',
xxxii.	        feedback: ''
xxxiii.	      });
xxxiv.	      alert('Thank you for your valuable feedback!');
xxxv.	    }
xxxvi.	  };
Copied!
•	This code contains:
o	const confirmationMessage = ...: This template constructs a confirmation message using the data from the formData object. It includes the name, email, and feedback fields the user enters.
o	const isConfirmed = window.confirm(...);: This line displays a confirmation dialog using the window.confirm(), presenting the confirmationMessage to the user. If the user confirms the details in the dialog, isConfirmed is set to true; otherwise, it's set to false.
o	if (isConfirmed) { ... }: This conditional statement checks if the user has confirmed their details by clicking "OK" in the confirmation dialog.
o	setFormData({ ... });: The setFormData function is called to reset the formData state to empty values, clearing the form fields after submission.
o	alert('Thank you for your valuable feedback!');: After resetting the form, an alert is displayed to the user thanking them for their feedback.
Note: Include this code just before the return of the FeedbackForm component.

Implement onSubmit event handler
1.	To submit the details, include the onSubmit event handler in the <form> tag.
1.	1
ii.	<form onSubmit={handleSubmit} className="feedback-form">
Copied!
Step 9: Check the output
1.	Now, you need to rerun the application again and fill the details. Then click Submit Feedback. A confirm box will appear with the filled details. If application is already running in browser, then just refresh the page.
 
2.	If you click OK, it will display another alert box with a thank you note.
 
3.	If you click Cancel in the confirm box, the form with filled details will reappear.
Congratulations! You have created a feedback form application!
4.	Click here for the entire code solution for FeedbackForm.jsx

lxx.	     import React, { useState } from 'react';
lxxi.	     import './FeedbackForm.css'; // Import CSS for styling
lxxii.	
lxxiii.	     const FeedbackForm = () => {
lxxiv.	         const [formData, setFormData] = useState({
lxxv.	             name: '',
lxxvi.	             email: '',
lxxvii.	             feedback: ''
lxxviii.	           });
lxxix.	           const handleChange = (event) => {
lxxx.	             const { name, value } = event.target;
lxxxi.	             setFormData({
lxxxii.	               ...formData,
lxxxiii.	               [name]: value
lxxxiv.	             });
lxxxv.	           };
lxxxvi.	           const handleSubmit = (event) => {
lxxxvii.	             event.preventDefault();
lxxxviii.	             const confirmationMessage = `
lxxxix.	               Name: ${formData.name}
xc.	               Email: ${formData.email}
xci.	               Feedback: ${formData.feedback}
xcii.	             `;
xciii.	             const isConfirmed = window.confirm(`Please confirm your details:\n\n${confirmationMessage}`);
xciv.	             if (isConfirmed) {
xcv.	               console.log('Submitting feedback:', formData);
xcvi.	               setFormData({
xcvii.	                 name: '',
xcviii.	                 email: '',
xcix.	                 feedback: ''
c.	               });
ci.	               alert('Thank you for your valuable feedback!');
cii.	             }
ciii.	           };
civ.	       return (
cv.	         <>
cvi.	         <nav>
cvii.	         Tell Us What You Think
cviii.	         </nav>
cix.	         <form onSubmit={handleSubmit} className="feedback-form">
cx.	             <h2>We'd Love to Hear From You!</h2>
cxi.	             <p>Please share your feedback with us.</p>
cxii.	             <input
cxiii.	               type="text"
cxiv.	               name="name"
cxv.	               placeholder="Your Name"
cxvi.	               value={formData.name}
cxvii.	               onChange={handleChange}
cxviii.	             />
cxix.	             <input
cxx.	               type="email"
cxxi.	               name="email"
cxxii.	               placeholder="Your Email"
cxxiii.	               value={formData.email}
cxxiv.	               onChange={handleChange}
cxxv.	             />
cxxvi.	             <textarea
cxxvii.	               name="feedback"
cxxviii.	               placeholder="Your Feedback"
cxxix.	               value={formData.feedback}
cxxx.	               onChange={handleChange}
cxxxi.	             ></textarea>
cxxxii.	             <button type="submit">Submit Feedback</button>
cxxxiii.	           </form>
cxxxiv.	         </>
cxxxv.	       );
cxxxvi.	     };
cxxxvii.	
cxxxviii.	     export default FeedbackForm;
Copied!
PreviousNext


Practice Exercise
1.	In this exercise you will create a rating system using radio buttons to let users provide rating as well.
2.	First you need to create one variable named rating within the formData useState hook and initialize it as empty string.
Hint: Include this variable as key value pair within formData
Click here for the solution
	
3.	For this you need to use input box with type radio button. To create a rating system using five radio buttons, where each radio button represents a rating value from 1 to 5. Each radio button should display its corresponding value: the first radio button showing “1”, the second showing “2”, and so on up to the fifth radio button displaying “5”. Make sure that input box with type radio button have onChange event handler to update the formData state to reflect the new selection made by the user using handleChange function.
Hint: Use input box filed with type='radio'. Call event handler function using onChange={handleChange}
Click here for the solution
	
4.	handleChange function will remain unchanges as you are taking the entire information using ...formData spread operator.
5.	Now you need to incorporate the rating details in the handleSubmit function. For this you need to take user selected value for rating from formData vraibale and include it in confirmationMessage to display along with other details.
Hint: Put formData.rating value in one variable to access and display user input for radio button filed
Click here for the solution
	
6.	Now check the output by re-running the application again. The output will look like according to given screenshot.
 
7.	Fill the entire form again and chekc the alert message. It will display rating along with other details as well.
 
Click here for the entire code solution

1.	import React, { useState } from 'react';
2.	import './FeedbackForm.css'; // Import CSS for styling
3.	
4.	const FeedbackForm = () => {
5.	    const [formData, setFormData] = useState({
6.	        name: '',
7.	        email: '',
8.	        feedback: '',
9.	        rating: '' // New state for rating
10.	    });
11.	
12.	    const handleChange = (event) => {
13.	        const { name, value } = event.target;
14.	        setFormData({
15.	            ...formData,
16.	            [name]: value
17.	        });
18.	    };
19.	
20.	    const handleSubmit = (event) => {
21.	        event.preventDefault();
22.	        const confirmationMessage = `
23.	          Name: ${formData.name}
24.	          Email: ${formData.email}
25.	          Feedback: ${formData.feedback}
26.	          Rating: ${formData.rating}
27.	        `;
28.	        const isConfirmed = window.confirm(`Please confirm your details:\n\n${confirmationMessage}`);
29.	        if (isConfirmed) {
30.	            console.log('Submitting feedback:', formData);
31.	            setFormData({
32.	                name: '',
33.	                email: '',
34.	                feedback: '',
35.	                rating: '' // Reset rating after submission
36.	            });
37.	            alert('Thank you for your valuable feedback!');
38.	        }
39.	    };
40.	  return (
41.	    <>
42.	    <nav>
43.	    Tell Us What You Think
44.	    </nav>
45.	    <form onSubmit={handleSubmit} className="feedback-form">
46.	        <h2>We'd Love to Hear From You!</h2>
47.	        <p>Please share your feedback with us.</p>
48.	        <input
49.	          type="text"
50.	          name="name"
51.	          placeholder="Your Name"
52.	          value={formData.name}
53.	          onChange={handleChange}
54.	        />
55.	        <input
56.	          type="email"
57.	          name="email"
58.	          placeholder="Your Email"
59.	          value={formData.email}
60.	          onChange={handleChange}
61.	        />
62.	        <textarea
63.	          name="feedback"
64.	          placeholder="Your Feedback"
65.	          value={formData.feedback}
66.	          onChange={handleChange}
67.	        ></textarea>
68.	         <div style={{display:'flex',gap:'10px',flexDirection:'column'}}>
69.	                    <span>Rate Us:</span>
70.	                    <p><input
71.	                        type="radio"
72.	                        name="rating"
73.	                        value="1"
74.	                       
75.	                        onChange={handleChange}
76.	                    /> 1</p>
77.	                  <p>  <input
78.	                        type="radio"
79.	                        name="rating"
80.	                        value="2"
81.	                        
82.	                        onChange={handleChange}
83.	                    /> 2</p>
84.	                  <p>  <input
85.	                        type="radio"
86.	                        name="rating"
87.	                        value="3"
88.	                        onChange={handleChange}
89.	                    /> 3</p>
90.	                   <p> <input
91.	                        type="radio"
92.	                        name="rating"
93.	                        value="4"
94.	                        onChange={handleChange}
95.	                    /> 4</p>
96.	                    <p><input
97.	                        type="radio"
98.	                        name="rating"
99.	                        value="5"
100.	                        onChange={handleChange}
101.	                    /> 5</p>
102.	                </div>
103.	        <button type="submit">Submit Feedback</button>
104.	      </form>
105.	    </>
106.	  );
107.	};
108.	
109.	export default FeedbackForm;
Copied!
PreviousNext

