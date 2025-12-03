<script>
    import {onMount} from 'svelte';

    let todoItem =$state('');
    let todoCategory = $state('');
    let todoList =$state([]);
    let giftList =$state([]);
    let decorList =$state([]);
    let foodList =$state([]);

    onMount(() => {
        let storedList = localStorage.getItem("storedList");
        if (storedList) {
            todoList = (JSON.parse(storedList));
        }
        sortLists();
    })

    function updateList() {
        return localStorage.setItem("storedList", JSON.stringify(todoList));
    }
    function sortLists() {
        giftList = todoList.filter(item => item.category == "gifts");
        decorList = todoList.filter(item => item.category == "decor");
        foodList = todoList.filter(item => item.category == "food");

    }
//add todoItem to todoList
    function addItem(event) {
        event.preventDefault();
        if (todoItem.trim().length === 0) {
            return;
        }
        todoList =[...todoList, {
            text: todoItem,
            done: false,
            category: todoCategory
        }];
        updateList();
        sortLists();
        todoItem ='';
    }
    //remove todoItem from todoList
    function removeItem(index) {
          todoList.splice(index,1);
          updateList();
          sortLists();
    }

</script>

    <form onsubmit={addItem}>
        <input type="text" bind:value={todoItem}>
        <div>
            <input type="radio" id="gifts"
            bind:group={todoCategory} value={"gifts"} />
            <label for="gifts">Gifts</label>
        </div>
         <div>
            <input type="radio" id="decor"
            bind:group={todoCategory} value={"decor"}/>
            <label for="decor">Decor</label>
        </div>
         <div>
            <input type="radio" id="food"
            bind:group={todoCategory} value={"food"} />
            <label for="food">Food</label>
        </div>
        <button type="submit">Add</button>
    </form>

    <div class="todo-lists">
    <div class="todo-list">
        <h2>Gifts</h2>
        <ul>
           {#each giftList as item, index}
                 <li>
                    <input type="checkbox" bind:checked={item.done} onchange={updateList}>
                    <span class:done={item.done}>{item.text}</span>
                    <button type="button" onclick={() => removeItem(index)}>x</button>
                </li>
           {/each}
        </ul>
    </div>
        <div class="todo-list">
            <h2>Decor</h2>
        <ul>
           {#each decorList as item, index}
                 <li>
                    <input type="checkbox" bind:checked={item.done} onchange={updateList}>
                    <span class:done={item.done}>{item.text}</span>
                    <button type="button" onclick={() => removeItem(index)}>x</button>
                </li>
           {/each}
        </ul>
    </div>
        <div class="todo-list">
            <h2>Food</h2>
        <ul>
           {#each foodList as item, index}
                 <li>
                    <input type="checkbox" bind:checked={item.done} onchange={updateList}>
                    <span class:done={item.done}>{item.text}</span>
                    <button type="button" onclick={() => removeItem(index)}>x</button>
                </li>
           {/each}
        </ul>
    </div>
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