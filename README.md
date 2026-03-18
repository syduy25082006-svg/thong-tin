<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trình Quản Lý Công Việc</title>
    <style>
        /* CSS để làm cho giao diện đẹp và hiện đại hơn */
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f4f7f6; display: flex; justify-content: center; padding: 50px; }
        .todo-container { background: white; padding: 2rem; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); width: 100%; max-width: 500px; }
        h2 { text-align: center; color: #333; }
        
        .input-group { display: flex; gap: 10px; margin-bottom: 20px; flex-wrap: wrap; }
        input[type="text"] { flex: 2; padding: 10px; border: 1px solid #ddd; border-radius: 6px; }
        input[type="date"] { flex: 1; padding: 10px; border: 1px solid #ddd; border-radius: 6px; }
        button#add-btn { padding: 10px 20px; background-color: #28a745; color: white; border: none; border-radius: 6px; cursor: pointer; transition: 0.3s; }
        button#add-btn:hover { background-color: #218838; }

        ul { list-style: none; padding: 0; }
        li { background: #fff; border-bottom: 1px solid #eee; padding: 12px; display: flex; align-items: center; justify-content: space-between; transition: 0.2s; }
        li:last-child { border-bottom: none; }
        .task-info { display: flex; align-items: center; gap: 15px; flex: 1; }
        .task-text { font-weight: 500; }
        .task-date { font-size: 0.85rem; color: #888; }
        
        /* Hiệu ứng khi hoàn thành */
        .completed .task-text { text-decoration: line-through; color: #bbb; }
        input[type="checkbox"] { transform: scale(1.2); cursor: pointer; }
        .delete-btn { color: #ff4d4d; border: none; background: none; cursor: pointer; font-size: 1.2rem; }
    </style>
</head>
<body>

<div class="todo-container">
    <h2>📝 My To-Do List</h2>
    
    <div class="input-group">
        <input type="text" id="task-input" placeholder="Nhập công việc...">
        <input type="date" id="date-input">
        <button id="add-btn">Thêm</button>
    </div>

    <ul id="todo-list">
        </ul>
</div>

<script>
    const taskInput = document.getElementById('task-input');
    const dateInput = document.getElementById('date-input');
    const addBtn = document.getElementById('add-btn');
    const todoList = document.getElementById('todo-list');

    // Hàm thêm công việc mới
    addBtn.addEventListener('click', () => {
        const taskValue = taskInput.value;
        const dateValue = dateInput.value;

        if (taskValue === '') {
            alert("Vui lòng nhập nội dung công việc!");
            return;
        }

        // Tạo phần tử li
        const li = document.createElement('li');
        
        li.innerHTML = `
            <div class="task-info">
                <input type="checkbox" class="complete-checkbox">
                <div>
                    <div class="task-text">${taskValue}</div>
                    <div class="task-date">${dateValue ? 'Hạn: ' + dateValue : 'Không có hạn'}</div>
                </div>
            </div>
            <button class="delete-btn">&times;</button>
        `;

        // Chức năng đánh dấu hoàn thành (ô tích)
        const checkbox = li.querySelector('.complete-checkbox');
        checkbox.addEventListener('change', () => {
            li.classList.toggle('completed');
        });

        // Chức năng xóa công việc
        const deleteBtn = li.querySelector('.delete-btn');
        deleteBtn.addEventListener('click', () => {
            li.remove();
        });

        todoList.appendChild(li);

        // Xóa nội dung input sau khi thêm
        taskInput.value = '';
        dateInput.value = '';
    });
</script>

</body>
</html>
