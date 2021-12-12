<script>
  import { createEventDispatcher } from "svelte";

  let dispatch = createEventDispatcher();
  let name;
  let beltColor;
  let age;
  // let fighting = false;
  // let sneaking = false;
  // let running = false;
  let skills = [];

  const handleSubmit = () => {
    console.log(name, beltColor, age, skills);
    const person = {
      name,
      beltColor,
      age,
      skills,
      id: Math.random()
    };
    dispatch("addPerson", person);
  };
</script>

<form on:submit|preventDefault={handleSubmit}>
  <div class="inputT">
    <span>Name</span>
    <input type="text" placeholder="name" bind:value={name} />
  </div>
  <div class="inputT">
    <span>age</span>
    <input type="number" placeholder="age" bind:value={age} />
  </div>
  <div class="inputT">
    <label for="">Skills:</label>
    <!-- <span><input type="checkbox" bind:checked={fighting} /> fighting</span>
      <span><input type="checkbox" bind:checked={sneaking} /> sneaking</span>
      <span><input type="checkbox" bind:checked={running} /> running</span> -->
    <span
      ><input type="checkbox" bind:group={skills} value="fighting" /> fighting</span
    >
    <span
      ><input type="checkbox" bind:group={skills} value="sneaking" /> sneaking</span
    >
    <span
      ><input type="checkbox" bind:group={skills} value="running" /> running</span
    >
  </div>
  <div class="inputT">
    <span>belt color</span>
    <select bind:value={beltColor}>
      <option value="black">Black</option>
      <option value="orange">Orange</option>
      <option value="brown">Brown</option>
      <option value="white">White</option>
    </select>
  </div>
  <button>Add Person</button>
</form>

<style>
  .inputT {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 15px 0;
    padding: 0 10px;
  }
</style>
