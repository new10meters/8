App.js 

import React from 'react'; 
import ReminderApp from './ReminderApp'; 
function App() { 
return ( 
<div className="App"> 
<ReminderApp /> 
</div> 
); 
} 
export default App; 


ReminderApp.js 

import React, { useState } from 'react'; 
import './ReminderApp.css'; 
function ReminderApp() {  
const [tasks, setTasks] = useState([]); 
const [taskName, setTaskName] = useState(''); 
const [dueDate, setDueDate] = useState(''); 
const [description, setDescription] = useState(''); 
const [filter, setFilter] = useState('all'); 
const addTask = () => { 
if (!taskName || !dueDate) { 
alert('Please fill in both task name and due date.'); 
return; 
} 
const newTask = { 
id: Date.now(), 
name: taskName, 
dueDate: dueDate, 
description: description, 
completed: false, 
};   
setTasks([...tasks, newTask]); 
setTaskName(''); 
setDueDate(''); 
setDescription(''); 
}; 
const toggleCompletion = (id) => { 
setTasks( 
tasks.map((task) => 
task.id === id ? { ...task, completed: !task.completed } : task 
) 
); 
}; 
const filteredTasks = tasks.filter((task) => { 
if (filter === 'all') return true; 
if (filter === 'completed') return task.completed; 
if (filter === 'notCompleted') return !task.completed; 
return true; 
}); 
return ( 
<div className="app-container"> 
<div className="task-form"> 
<h2 className="form-title">Add Task</h2> 
<div className="form-inputs"> 
<input 
type="text" 
placeholder="Task Name" 
value={taskName} 
onChange={(e) => setTaskName(e.target.value)} 
className="input" 
/> 
<input 
type="date" 
value={dueDate} 
onChange={(e) => setDueDate(e.target.value)} 
className="input" 
/> 
<textarea 
placeholder="Description (optional)" 
value={description} 
onChange={(e) => setDescription(e.target.value)} 
className="textarea" 
></textarea> 
</div> 
<button onClick={addTask} className="button"> 
Add Task 
</button> 
</div> 
<div className="task-filter"> 
<h2 className="filter-title">Filter Tasks</h2> 
<select 
onChange={(e) => setFilter(e.target.value)} 
value={filter} 
className="select" 
> 
<option value="all">All Tasks</option> 
<option value="completed">Completed</option> 
<option value="notCompleted">Not Completed</option> 
</select> 
</div> 
<div> 
{filteredTasks.length ? ( 
filteredTasks.map((task) => ( 
<div className="task-item"> 
<div> 
<h3 className="task-name">{task.name}</h3> 
<p>Due: {task.dueDate}</p> 
{task.description && <p>{task.description}</p>} 
</div> 
<label> 
<input 
type="checkbox" 
checked={task.completed} 
onChange={() => toggleCompletion(task.id)} 
className="checkbox" 
/> 
{task.completed ? 'Completed' : 'Mark as Completed'} 
</label> 
</div> 
)) 
) : ( 
<p>No tasks available.</p> 
)} 
</div> 
</div> 
); 
}; 
export default ReminderApp; 


ReminderApp.css 

.app-container { 
max-width: 600px; 
margin: 0 auto; 
padding: 20px; 
} 
.task-form, 
.task-filter { 
margin-bottom: 20px; 
padding: 20px; 
border: 1px solid #ccc; 
border-radius: 8px; 
} 
.form-title, 
.filter-title { 
font-size: 1.5rem; 
font-weight: bold; 
margin-bottom: 10px; 
} 
.form-inputs { 
display:flex; 
flex-direction:column; 
gap: 10px; 
} 
.input, 
.textarea, 
.select { 
padding: 10px; 
font-size: 1rem; 
border-radius: 4px; 
border: 1px solid #ccc; 
} 
.button { 
margin-top: 10px; 
padding: 10px 20px; 
font-size: 1rem; 
border-radius: 4px; 
border: none; 
background-color: #007bff; 
color: #fff; 
cursor: pointer; 
} 
.task-item { 
margin-bottom: 10px; 
padding: 10px; 
border: 1px solid #ccc; 
border-radius: 8px; 
display: flex; 
justify-content: space-between; 
align-items: center; 
} 
.task-name { 
font-size: 1.25rem; 
font-weight: bold; 
} 
.checkbox { 
margin-right: 10px; 
} 
Diagrams are not compulsory  
