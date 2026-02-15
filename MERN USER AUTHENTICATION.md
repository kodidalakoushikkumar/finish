## Steps to Create the Project:

### Setting up Backend (server)

Step 1: Create a new project and navigate to folder :

```
mkdir server  
cd server
```

Step 2: Initialize Node.js backend:

```
npm init -y
```

Step 3: Install all required dependencies:

```
npm install express mongoose bcryptjs jsonwebtoken cors
```

### Project Structure(Backend):

![Screenshot-2024-03-19-111054](https://media.geeksforgeeks.org/wp-content/uploads/20240319111239/Screenshot-2024-03-19-111054.png "Click to enlarge")

The updated dependencies in package.json file of server will look like:

```
"dependencies": {  
    "bcryptjs": "^2.4.3",  
    "cors": "^2.8.5",  
    "express": "^4.18.3",  
    "jsonwebtoken": "^9.0.2",  
    "mongoose": "^8.2.2"  
}
```

- Data Stored in Database

![Screenshot-2024-03-19-112229](https://media.geeksforgeeks.org/wp-content/uploads/20240319112321/Screenshot-2024-03-19-112229.png "Click to enlarge")

Create index.js and config.js write the below code.
Create folder routes with file auth.js and another folder models with file User.js

```
// server/index.js
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
const config = require('./config');
const authRoutes = require('./routes/auth');

const app = express();

app.use(express.json());
app.use(cors());

mongoose.connect(config.mongoURI, { useNewUrlParser: true, 
                                    useUnifiedTopology: true })
    .then(() => console.log('MongoDB Connected'))
    .catch(err => console.error(err));

app.use('/api/auth', authRoutes);

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => console.log(`Server started on port ${PORT}`));
```

```
// server/config.js
module.exports = {
    mongoURI: 'yourmongourl',
    jwtSecret: 'hello'
};
```

```
// server/models/User.js
const mongoose = require('mongoose');

const UserSchema = new mongoose.Schema({
    username: {
        type: String,
        required: true,
        unique: true
    },
    password: {
        type: String,
        required: true
    }
});

module.exports = mongoose.model('User', UserSchema);
```

```
// server/routes/auth.js
const express = require('express');
const router = express.Router();
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const config = require('../config');
const User = require('../models/User');

// Register Route
router.post('/register', async (req, res) => {
    const { username, password } = req.body;

    try {
        let user = await User.findOne({ username });
        if (user) {
            return res.status(400).json({ msg: 'User already exists' });
        }

        user = new User({ username, password });

        const salt = await bcrypt.genSalt(10);
        user.password = await bcrypt.hash(password, salt);

        await user.save();

        const payload = {
            user: { id: user.id }
        };

        jwt.sign(payload, config.jwtSecret, { expiresIn: 3600 }, 
        (err, token) => {
            if (err) throw err;
            res.json({ token });
        });
    } catch (err) {
        console.error(err.message);
        res.status(500).send('Server Error');
    }
});

router.post('/login', async (req, res) => {
    const { username, password } = req.body;

    try {
        // Check if the user exists
        let user = await User.findOne({ username });
        if (!user) {
            return res.status(400).json({ msg: 'Invalid credentials' });
        }

        // Validate password
        const isMatch = await bcrypt.compare(password, user.password);
        if (!isMatch) {
            return res.status(400).json({ msg: 'Invalid credentials' });
        }

        // Generate JWT token
        const payload = {
            user: {
                id: user.id
            }
        };

        jwt.sign(payload, config.jwtSecret, { expiresIn: 3600 }, 
        (err, token) => {
            if (err) throw err;
            res.json({ token });
        });
    } catch (err) {
        console.error(err.message);
        res.status(500).send('Server Error');
    }
});

module.exports = router;
```

Start the backend server with the following command:

```
node index.js
```

### Setting up Frontend (client)

Step 1: Set up React frontend using the command.

```
npx create-react-app client  
cd client
```

Step 2: Install the required dependencies.

```
npm install axios
```

### Project Structure(Frontend):

![Screenshot-2024-03-19-111105](https://media.geeksforgeeks.org/wp-content/uploads/20240319111319/Screenshot-2024-03-19-111105.png "Click to enlarge")

The updated dependencies in package.json file of client will look like:

```
"dependencies": {  
    "@testing-library/jest-dom": "^5.17.0",  
    "@testing-library/react": "^13.4.0",  
    "@testing-library/user-event": "^13.5.0",  
    "axios": "^1.6.8",  
    "react": "^18.2.0",  
    "react-dom": "^18.2.0",  
    "react-scripts": "5.0.1",  
    "web-vitals": "^2.1.4"  
},
```

Create file Register.js and Login.js
Replace code of App.js and index.js

```
/* client/src/components/style.css */
.auth-form {
    width: 300px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.auth-form h2 {
    margin-top: 0;
}

.auth-form input {
    width: 100%;
    margin-bottom: 10px;
    padding: 8px;
    border-radius: 3px;
    border: 1px solid #ccc;
}

.auth-form button {
    width: 100%;
    padding: 10px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 3px;
    cursor: pointer;
}

.auth-form button:hover {
    background-color: #0056b3;
}

.message {
    margin-top: 10px;
    color: green;
}
```

```
// client/src/components/Login.js
import React, { useState } from 'react';
import axios from 'axios';
import './style.css'; // Import CSS for styling

const Login = ({ setLoggedInUser }) => {
    const [formData, setFormData] = useState({
        username: '',
        password: ''
    });
    const [message, setMessage] = useState('');

    const { username, password } = formData;

    const onChange = e => setFormData({ ...formData, 
                                      [e.target.name]: e.target.value });

    const onSubmit = async e => {
        e.preventDefault();
        try {
            const res = 
                await axios.post('http://localhost:5000/api/auth/login', 
            {
                username,
                password
            });
            localStorage.setItem('token', res.data.token);
            setLoggedInUser(username);
            
            // Set success message
            setMessage('Logged in successfully');
        } catch (err) {
            console.error(err.response.data);
            // Set error message
            setMessage('Failed to login - wrong credentials');         
        }
    };

    return (
        <div className="auth-form">
            <h2>Login</h2>
            <form onSubmit={onSubmit}>
                <input type="text" 
                       placeholder="Username" 
                       name="username" 
                       value={username} 
                       onChange={onChange} 
                       required />
                <input type="password" 
                       placeholder="Password" 
                       name="password" 
                       value={password} 
                       onChange={onChange} 
                       required />
                <button type="submit">Login</button>
            </form>
            <p className="message">{message}</p>
        </div>
    );
};

export default Login;
```

```
// client/src/components/Register.js
import React, { useState } from 'react';
import axios from 'axios';
import './style.css'; // Import CSS for styling

const Register = () => {
    const [formData, setFormData] = useState({
        username: '',
        password: ''
    });
    const [message, setMessage] = useState('');

    const { username, password } = formData;

    const onChange = e => setFormData({ ...formData, [e.target.name]: e.target.value });

    const onSubmit = async e => {
        e.preventDefault();
        try {
            const res = await axios.post('http://localhost:5000/api/auth/register', {
                username,
                password
            });
            setMessage('Registered successfully'); // Set success message
        } catch (err) {
            console.error(err.response.data);
            setMessage('Failed to register, User already exists'); // Set error message
        }
    };

    return (
        <div className="auth-form">
            <h2>Register</h2>
            <form onSubmit={onSubmit}>
                <input type="text" placeholder="Username" name="username" value={username} onChange={onChange} required />
                <input type="password" placeholder="Password" name="password" value={password} onChange={onChange} required />
                <button type="submit">Register</button>
            </form>
            <p className="message">{message}</p>
        </div>
    );
};

export default Register;
```

```
// client/src/App.js
import React, { useState } from 'react';
import Register from './components/Register';
import Login from './components/Login';

const App = () => {
    const [loggedInUser, setLoggedInUser] = useState(null);

    const handleLogout = () => {
        localStorage.removeItem('token'); // Remove token from localStorage
        setLoggedInUser(null); // Set logged-in user to null
    };

    return (
        <div className="App">
            
            {loggedInUser ? (
                <div>
                    <p>Welcome {loggedInUser}</p>
                    <button onClick={handleLogout}>Logout</button>
                </div>
            ) : (
                <div>
                    <Register />
                    <Login setLoggedInUser={setLoggedInUser} />
                </div>
            )}
        </div>
    );
};

export default App;
```

```
// client/src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>,
    document.getElementById('root')
);
```

To start frontend code:

```
npm start
```

Output:

![uu](https://media.geeksforgeeks.org/wp-content/uploads/20240319112149/uu.gif "Click to enlarge")