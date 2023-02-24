<script>
    let tasks = [
      { id: 1, text: 'Learn SvelteKit', done: false },
      { id: 2, text: 'Build a todo app', done: true },
      { id: 3, text: 'Deploy to production', done: false },
    ];
  
    function addTask(event) {
      event.preventDefault();
      const input = event.target.querySelector('input[type="text"]');
      const taskText = input.value.trim();
      if (taskText.length === 0) return;
      const newTask = {
        id: tasks.length + 1,
        text: taskText,
        done: false,
      };
      tasks = [...tasks, newTask];
      input.value = '';
    }
  
    function toggleTaskDone(taskId) {
      tasks = tasks.map((task) =>
        task.id === taskId ? { ...task, done: !task.done } : task
      );
    }
  
    function deleteTask(taskId) {
      tasks = tasks.filter((task) => task.id !== taskId);
    }
  </script>
  

<div>
    <div class="flex flex-col items-center text-xl">
      <!-- <h1 class="text-3xl font-bold mb-4">Todo List</h1> -->
      <form on:submit={addTask}>
        <input type="text" placeholder="Add a new task" class="w-80 border-2 rounded-lg px-4 py-2 mb-4" />
        <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Add Task</button>
      </form>
      <ul class="w-full max-w-md mb-8">
        {#each tasks as task (task.id)}
          <li class="bg-opacity-20 bg-white backdrop-blur-lg rounded drop-shadow-lg shadow-md my-4 mb-4 p-4 flex justify-between items-center transition duration-150" class:done={task.done}>
            <span class="text-lg">{task.text}</span>
            <div class="flex items-center ">
              <button on:click={() => toggleTaskDone(task.id)} class="{task.done ? 'bg-yellow-500 hover:bg-yellow-700 ' : '  bg-green-500 hover:bg-green-700'} text-white font-bold py-2 px-4 rounded mr-2">{task.done ? 'Undone' : 'Done'}</button>
              <button on:click={() => deleteTask(task.id)} class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded">Delete</button>
            </div>
          </li>
        {/each}
      </ul>
    </div>
  </div>
  