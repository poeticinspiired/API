Here is one of my API samples with steps and guidelines: 
1.	First, I will create a new directory in my project: 

	mkdir restful-api
	cd restful-api
	Then, Initialize a new Node.js project:
	npm init -y
	Install Express.js:
	npm install express

2.	File: // index.js
const express = require('express');
const app = express();
const PORT = 3000;
// Middleware to parse JSON bodies
app.use(express.json());
// Sample data (for demonstration purposes)
let users = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Jane' },
];
// GET all users
app.get('/api/users', (req, res) => {
  res.json(users);
});
// GET user by ID
app.get('/api/users/:id', (req, res) => {
  const user = users.find(user => user.id === parseInt(req.params.id));
  if (!user) return res.status(404).send('User not found');
  res.json(user);
});
// POST a new user
app.post('/api/users', (req, res) => {
  const newUser = {
    id: users.length + 1,
    name: req.body.name
  };
  users.push(newUser);
  res.status(201).json(newUser);
})
// PUT update user by ID
app.put('/api/users/:id', (req, res) => {
  const user = users.find(user => user.id === parseInt(req.params.id));
  if (!user) return res.status(404).send('User not found');
  user.name = req.body.name;
  res.json(user);
});
// DELETE user by ID
app.delete('/api/users/:id', (req, res) => {
  const userIndex = users.findIndex(user => user.id === parseInt(req.params.id));
  if (userIndex === -1) return res.status(404).send('User not found'); 
  users.splice(userIndex, 1);
  res.send('User deleted successfully');
});
// Start the server
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});

# API
