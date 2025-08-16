
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced To-Do List</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 700px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 30px;
            font-size: 2.2em;
            font-weight: 600;
        }

        .add-task-form {
            background: white;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
        }

        .form-row {
            display: flex;
            gap: 15px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }

        .form-group {
            display: flex;
            flex-direction: column;
            flex: 1;
            min-width: 150px;
        }

        .form-group label {
            font-size: 12px;
            font-weight: 600;
            color: #666;
            margin-bottom: 5px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        #taskInput {
            padding: 12px;
            border: 2px solid #e1e5e9;
            border-radius: 8px;
            font-size: 16px;
            transition: all 0.3s ease;
            outline: none;
        }

        #taskInput:focus {
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        select, input[type="date"] {
            padding: 10px;
            border: 2px solid #e1e5e9;
            border-radius: 8px;
            font-size: 14px;
            background: white;
            transition: all 0.3s ease;
            outline: none;
        }

        select:focus, input[type="date"]:focus {
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        #addBtn {
            padding: 12px 25px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s ease;
            align-self: flex-end;
        }

        #addBtn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(102, 126, 234, 0.4);
        }

        .filters {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            align-items: center;
        }

        .filter-group {
            display: flex;
            flex-direction: column;
        }

        .filter-group label {
            font-size: 12px;
            font-weight: 600;
            color: #666;
            margin-bottom: 3px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .filter-group select {
            padding: 8px 10px;
            font-size: 13px;
            min-width: 120px;
        }

        .task-counter {
            text-align: center;
            margin-bottom: 20px;
            color: #666;
            font-size: 14px;
        }

        .task-list {
            list-style: none;
        }

        .task-item {
            background: white;
            margin-bottom: 15px;
            padding: 20px;
            border-radius: 15px;
            border-left: 5px solid #ddd;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            transition: all 0.3s ease;
            animation: slideIn 0.5s ease;
        }

        .task-item:hover {
            transform: translateX(3px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.12);
        }

        .task-item.high-priority {
            border-left-color: #ff4757;
        }

        .task-item.medium-priority {
            border-left-color: #ffa502;
        }

        .task-item.low-priority {
            border-left-color: #2ed573;
        }

        .task-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 10px;
        }

        .task-text {
            font-size: 16px;
            color: #333;
            margin-bottom: 5px;
            word-break: break-word;
            line-height: 1.4;
        }

        .task-text.editing {
            display: none;
        }

        .task-edit-input {
            display: none;
            width: 100%;
            padding: 8px;
            border: 2px solid #667eea;
            border-radius: 6px;
            font-size: 16px;
            margin-bottom: 5px;
        }

        .task-edit-input.editing {
            display: block;
        }

        .task-meta {
            display: flex;
            gap: 15px;
            align-items: center;
            flex-wrap: wrap;
            margin-bottom: 10px;
        }

        .priority-badge {
            padding: 4px 8px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .priority-high {
            background: #ff4757;
            color: white;
        }

        .priority-medium {
            background: #ffa502;
            color: white;
        }

        .priority-low {
            background: #2ed573;
            color: white;
        }

        .category-badge {
            background: #667eea;
            color: white;
            padding: 4px 8px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: 500;
        }

        .due-date {
            color: #666;
            font-size: 13px;
        }

        .due-date.overdue {
            color: #ff4757;
            font-weight: 600;
        }

        .due-date.today {
            color: #ffa502;
            font-weight: 600;
        }

        .task-actions {
            display: flex;
            gap: 8px;
        }

        .btn {
            padding: 6px 12px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
            font-weight: 500;
            transition: all 0.3s ease;
        }

        .btn-edit {
            background: #3742fa;
            color: white;
        }

        .btn-delete {
            background: #ff4757;
            color: white;
        }

        .btn-save {
            background: #2ed573;
            color: white;
        }

        .btn-cancel {
            background: #747d8c;
            color: white;
        }

        .btn:hover {
            transform: translateY(-1px);
            filter: brightness(110%);
        }

        .empty-state {
            text-align: center;
            color: #666;
            font-size: 18px;
            margin-top: 50px;
            opacity: 0.7;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateX(-20px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        @media (max-width: 768px) {
            .container {
                margin: 0;
                border-radius: 0;
                min-height: 100vh;
                padding: 20px;
            }

            .form-row {
                flex-direction: column;
            }

            .form-group {
                min-width: auto;
            }

            .filters {
                flex-direction: column;
                align-items: stretch;
            }

            .filter-group select {
                min-width: auto;
            }

            .task-header {
                flex-direction: column;
                align-items: stretch;
            }

            .task-actions {
                margin-top: 10px;
            }

            .task-meta {
                flex-direction: column;
                align-items: flex-start;
                gap: 8px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>✨ Advanced To-Do List</h1>
        
        <div class="add-task-form">
            <div class="form-row">
                <div class="form-group" style="flex: 2;">
                    <label for="taskInput">Task Description</label>
                    <input type="text" id="taskInput" placeholder="What needs to be done?" maxlength="200">
                </div>
            </div>
            <div class="form-row">
                <div class="form-group">
                    <label for="prioritySelect">Priority</label>
                    <select id="prioritySelect">
                        <option value="medium">Medium</option>
                        <option value="high">High</option>
                        <option value="low">Low</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="categorySelect">Category</label>
                    <select id="categorySelect">
                        <option value="personal">Personal</option>
                        <option value="work">Work</option>
                        <option value="health">Health</option>
                        <option value="shopping">Shopping</option>
                        <option value="study">Study</option>
                        <option value="other">Other</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="dueDateInput">Due Date</label>
                    <input type="date" id="dueDateInput">
                </div>
                <div class="form-group">
                    <label>&nbsp;</label>
                    <button id="addBtn">Add Task</button>
                </div>
            </div>
        </div>

        <div class="filters">
            <div class="filter-group">
                <label for="filterPriority">Filter by Priority</label>
                <select id="filterPriority">
                    <option value="all">All Priorities</option>
                    <option value="high">High Priority</option>
                    <option value="medium">Medium Priority</option>
                    <option value="low">Low Priority</option>
                </select>
            </div>
            <div class="filter-group">
                <label for="filterCategory">Filter by Category</label>
                <select id="filterCategory">
                    <option value="all">All Categories</option>
                    <option value="personal">Personal</option>
                    <option value="work">Work</option>
                    <option value="health">Health</option>
                    <option value="shopping">Shopping</option>
                    <option value="study">Study</option>
                    <option value="other">Other</option>
                </select>
            </div>
            <div class="filter-group">
                <label for="sortBy">Sort by</label>
                <select id="sortBy">
                    <option value="created">Date Created</option>
                    <option value="priority">Priority</option>
                    <option value="duedate">Due Date</option>
                    <option value="category">Category</option>
                </select>
            </div>
        </div>

        <div class="task-counter">
            <span id="taskCount">0 tasks</span>
        </div>

        <ul class="task-list" id="taskList">
            <div class="empty-state" id="emptyState">
                No tasks yet! Add one above to get started. 🚀
            </div>
        </ul>
    </div>

    <script>
        let tasks = [];
        let taskIdCounter = 1;

        const taskInput = document.getElementById('taskInput');
        const prioritySelect = document.getElementById('prioritySelect');
        const categorySelect = document.getElementById('categorySelect');
        const dueDateInput = document.getElementById('dueDateInput');
        const addBtn = document.getElementById('addBtn');
        const taskList = document.getElementById('taskList');
        const emptyState = document.getElementById('emptyState');
        const taskCount = document.getElementById('taskCount');
        const filterPriority = document.getElementById('filterPriority');
        const filterCategory = document.getElementById('filterCategory');
        const sortBy = document.getElementById('sortBy');

        function updateTaskCount() {
            const filteredTasks = getFilteredTasks();
            const count = filteredTasks.length;
            taskCount.textContent = count === 1 ? '1 task' : `${count} tasks`;
        }

        function addTask() {
            const taskText = taskInput.value.trim();
            
            if (taskText === '') {
                taskInput.focus();
                return;
            }

            const task = {
                id: taskIdCounter++,
                text: taskText,
                priority: prioritySelect.value,
                category: categorySelect.value,
                dueDate: dueDateInput.value || null,
                createdAt: new Date(),
                isEditing: false
            };

            tasks.push(task);
            clearForm();
            renderTasks();
            taskInput.focus();
        }

        function clearForm() {
            taskInput.value = '';
            prioritySelect.value = 'medium';
            categorySelect.value = 'personal';
            dueDateInput.value = '';
        }

        function deleteTask(taskId) {
            tasks = tasks.filter(task => task.id !== taskId);
            renderTasks();
        }

        function editTask(taskId) {
            const task = tasks.find(t => t.id === taskId);
            if (task) {
                task.isEditing = true;
                renderTasks();
            }
        }

        function saveTask(taskId) {
            const task = tasks.find(t => t.id === taskId);
            const editInput = document.querySelector(`#edit-input-${taskId}`);
            
            if (task && editInput) {
                const newText = editInput.value.trim();
                if (newText !== '') {
                    task.text = newText;
                }
                task.isEditing = false;
                renderTasks();
            }
        }

        function cancelEdit(taskId) {
            const task = tasks.find(t => t.id === taskId);
            if (task) {
                task.isEditing = false;
                renderTasks();
            }
        }

        function getFilteredTasks() {
            let filteredTasks = [...tasks];

            // Filter by priority
            if (filterPriority.value !== 'all') {
                filteredTasks = filteredTasks.filter(task => task.priority === filterPriority.value);
            }

            // Filter by category
            if (filterCategory.value !== 'all') {
                filteredTasks = filteredTasks.filter(task => task.category === filterCategory.value);
            }

            // Sort tasks
            filteredTasks.sort((a, b) => {
                switch (sortBy.value) {
                    case 'priority':
                        const priorityOrder = { high: 3, medium: 2, low: 1 };
                        return priorityOrder[b.priority] - priorityOrder[a.priority];
                    case 'duedate':
                        if (!a.dueDate && !b.dueDate) return b.createdAt - a.createdAt;
                        if (!a.dueDate) return 1;
                        if (!b.dueDate) return -1;
                        return new Date(a.dueDate) - new Date(b.dueDate);
                    case 'category':
                        return a.category.localeCompare(b.category);
                    default: // created
                        return b.createdAt - a.createdAt;
                }
            });

            return filteredTasks;
        }

        function formatDueDate(dueDate) {
            if (!dueDate) return null;

            const today = new Date();
            const due = new Date(dueDate);
            const diffTime = due - today;
            const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));

            let className = '';
            let text = '';

            if (diffDays < 0) {
                className = 'overdue';
                text = `Overdue by ${Math.abs(diffDays)} day${Math.abs(diffDays) !== 1 ? 's' : ''}`;
            } else if (diffDays === 0) {
                className = 'today';
                text = 'Due Today';
            } else if (diffDays === 1) {
                text = 'Due Tomorrow';
            } else {
                text = `Due in ${diffDays} days`;
            }

            return { className, text };
        }

        function renderTasks() {
            taskList.innerHTML = '';
            const filteredTasks = getFilteredTasks();
            
            if (filteredTasks.length === 0) {
                taskList.appendChild(emptyState);
                updateTaskCount();
                return;
            }

            filteredTasks.forEach(task => {
                const taskItem = document.createElement('li');
                taskItem.className = `task-item ${task.priority}-priority`;

                const dueDateInfo = formatDueDate(task.dueDate);
                const dueDateHtml = dueDateInfo ? 
                    `<span class="due-date ${dueDateInfo.className}">📅 ${dueDateInfo.text}</span>` : '';

                taskItem.innerHTML = `
                    <div class="task-header">
                        <div>
                            <div class="task-text ${task.isEditing ? 'editing' : ''}">${escapeHtml(task.text)}</div>
                            <input type="text" class="task-edit-input ${task.isEditing ? 'editing' : ''}" 
                                   id="edit-input-${task.id}" value="${escapeHtml(task.text)}">
                            <div class="task-meta">
                                <span class="priority-badge priority-${task.priority}">${task.priority}</span>
                                <span class="category-badge">${task.category}</span>
                                ${dueDateHtml}
                            </div>
                        </div>
                        <div class="task-actions">
                            ${task.isEditing ? 
                                `<button class="btn btn-save" onclick="saveTask(${task.id})">Save</button>
                                 <button class="btn btn-cancel" onclick="cancelEdit(${task.id})">Cancel</button>` :
                                `<button class="btn btn-edit" onclick="editTask(${task.id})">Edit</button>
                                 <button class="btn btn-delete" onclick="deleteTask(${task.id})">Delete</button>`
                            }
                        </div>
                    </div>
                `;
                taskList.appendChild(taskItem);
            });

            updateTaskCount();
        }

        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        // Event listeners
        addBtn.addEventListener('click', addTask);

        taskInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                addTask();
            }
        });

        // Filter and sort event listeners
        filterPriority.addEventListener('change', renderTasks);
        filterCategory.addEventListener('change', renderTasks);
        sortBy.addEventListener('change', renderTasks);

        // Handle edit input enter key
        document.addEventListener('keypress', function(e) {
            if (e.key === 'Enter' && e.target.classList.contains('task-edit-input')) {
                const taskId = parseInt(e.target.id.replace('edit-input-', ''));
                saveTask(taskId);
            }
        });

        // Focus on input when page loads
        window.addEventListener('load', function() {
            taskInput.focus();
        });

        // Initial render
        renderTasks();
    </script>
</body>
</html>
