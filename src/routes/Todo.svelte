<script>
    let todoItem =$state('');
    let todoList =$state([]);
//add todoItem to todoList
    function addItem(event) {
        event.preventDefault();
        if (todoItem.trim().length === 0) {
            return;
        }
        todoList =[...todoList, {
            text: todoItem,
            done: false
        }];
        todoItem ='';
    }
    //remove todoItem from todoList
    function removeItem(index) {
          todoList.splice(index,1);
    }

</script>

    <form onsubmit={addItem}>
        <input type="text" bind:value={todoItem}>
        <button type="submit">Add</button>
    </form>

    <div class="todo-list">
        <ul>
           {#each todoList as item, index}
                 <li>
                    <input type="checkbox" bind:checked={item.done}>
                    <span class:done={item.done}>{item.text}</span>
                    <button type="button" onclick={() => removeItem(index)}>x</button>
                </li>
           {/each}
        </ul>
    </div>




<style>
    ul {
        list-style: none;
    }
    input[type="checkbox"] {
        height: 20px;
        width: 20px;
        accent-color: green;
    }
    li span.done {
         text-decoration: line-through;
         color: darkgrey;
    }
</style>