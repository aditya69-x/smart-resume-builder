<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Resume Builder</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }

        body {
            background-color: #f5f5f5;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            padding: 30px 0;
            background-color: #2c3e50;
            color: white;
            margin-bottom: 30px;
        }

        .form-section {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }

        input, textarea, select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            margin-bottom: 10px;
        }

        .btn {
            background-color: #3498db;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }

        .btn:hover {
            background-color: #2980b9;
        }

        .template-selection {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        .template-card {
            border: 1px solid #ddd;
            padding: 10px;
            border-radius: 4px;
            text-align: center;
            cursor: pointer;
        }

        .template-card.selected {
            border-color: #3498db;
            background-color: #f7f9fc;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>Smart Resume Builder</h1>
        <p>Create a professional resume in minutes</p>
    </div>

    <div class="container">
        <div class="form-section">
            <h2>Choose Template</h2>
            <div class="template-selection">
                <div class="template-card">
                    <img src="template1.jpg" alt="Template 1" style="width: 100%; height: auto;">
                    <p>Professional Template</p>
                </div>
                <div class="template-card">
                    <img src="template2.jpg" alt="Template 2" style="width: 100%; height: auto;">
                    <p>Creative Template</p>
                </div>
                <div class="template-card">
                    <img src="template3.jpg" alt="Template 3" style="width: 100%; height: auto;">
                    <p>Modern Template</p>
                </div>
            </div>
        </div>

        <div class="form-section">
            <h2>Personal Information</h2>
            <div class="form-group">
                <label for="fullName">Full Name</label>
                <input type="text" id="fullName" placeholder="Enter your full name">
            </div>
            <div class="form-group">
                <label for="email">Email</label>
                <input type="email" id="email" placeholder="Enter your email">
            </div>
            <div class="form-group">
                <label for="phone">Phone</label>
                <input type="tel" id="phone" placeholder="Enter your phone number">
            </div>
            <div class="form-group">
                <label for="address">Address</label>
                <textarea id="address" rows="3" placeholder="Enter your address"></textarea>
            </div>
        </div>

        <div class="form-section">
            <h2>Professional Summary</h2>
            <div class="form-group">
                <label for="summary">Career Summary</label>
                <textarea id="summary" rows="4" placeholder="Write a brief summary of your professional background"></textarea>
            </div>
        </div>

        <div class="form-section">
            <h2>Work Experience</h2>
            <div class="form-group">
                <label for="jobTitle">Job Title</label>
                <input type="text" id="jobTitle" placeholder="Enter job title">
                
                <label for="company">Company</label>
                <input type="text" id="company" placeholder="Enter company name">
                
                <label for="workDates">Dates</label>
                <input type="text" id="workDates" placeholder="MM/YYYY - MM/YYYY">
                
                <label for="responsibilities">Responsibilities</label>
                <textarea id="responsibilities" rows="4" placeholder="List your key responsibilities and achievements"></textarea>
            </div>
            <button class="btn" onclick="addMoreExperience()">+ Add More Experience</button>
        </div>

        <div class="form-section">
            <h2>Education</h2>
            <div class="form-group">
                <label for="degree">Degree</label>
                <input type="text" id="degree" placeholder="Enter degree/certification">
                
                <label for="school">School</label>
                <input type="text" id="school" placeholder="Enter school name">
                
                <label for="graduationDate">Graduation Date</label>
                <input type="text" id="graduationDate" placeholder="MM/YYYY">
            </div>
            <button class="btn" onclick="addMoreEducation()">+ Add More Education</button>
        </div>

        <div class="form-section">
            <h2>Skills</h2>
            <div class="form-group">
                <label for="skills">Skills</label>
                <textarea id="skills" rows="3" placeholder="Enter your skills (separated by commas)"></textarea>
            </div>
        </div>

        <div style="text-align: center; margin-top: 30px;">
            <button class="btn" onclick="generateResume()">Generate Resume</button>
        </div>
    </div>

    <script>
        function addMoreExperience() {
            // Add functionality to duplicate work experience section
        }

        function addMoreEducation() {
            // Add functionality to duplicate education section
        }

        function generateResume() {
            // Add functionality to generate the resume
        }
    </script>
</body>
</html>
# smart-resume-builder
const express = require('express');
const mysql = require('mysql2');
const bodyParser = require('body-parser');

const app = express();
const port = process.env.PORT || 3000;

// Middleware
app.use(bodyParser.json());
app.use(express.static('public')); // Serve static files from public directory

// MySQL connection
const db = mysql.createConnection({
    host: 'localhost',
    user: 'root', // your mysql username
    password: '', // your mysql password
    database: 'resume_builder' // your mysql database name
});

db.connect(err => {
    if(err) throw err;
    console.log('Connected to MySQL');
});

// API route to save resume data
app.post('/api/resume', (req, res) => {
    const { name, email, phone, skills, experience } = req.body;

    const sql = 'INSERT INTO resumes (name, email, phone, skills, experience) VALUES (?, ?, ?, ?, ?)';
    db.query(sql, [name, email, phone, JSON.stringify(skills), JSON.stringify(experience)], (err, results) => {
        if(err) {
            res.status(500).json({ success: false, message: 'Error saving to database' });
            return;
        }
        res.json({ success: true, resumeData: { name, email, phone, skills, experience }});
    });
});

// Start the server
app.listen(port, () => {
    console.log(`Server running on port ${port}`);
});
CREATE TABLE resumes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    phone VARCHAR(20) NOT NULL,
    skills TEXT NOT NULL,
    experience TEXT NOT NULL
);
npm install -g firebase-tools
