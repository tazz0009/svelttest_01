<script>
  import Modal from "./Modal.svelte";
  import AddPersonForm from "./AddPersonForm.svelte";

  let showModal = false;

  let people = [
    { name: "yoshi", beltColor: "black", age: 25, id: 1 },
    { name: "mario", beltColor: "orange", age: 45, id: 2 },
    { name: "luigi", beltColor: "brown", age: 35, id: 3 }
  ];

  const handleClick = (id) => {
    people = people.filter((person) => {
      person.id != id;
    });
  };

  const toggleModal = () => {
    showModal = !showModal;
  };

  const addPerson = (e) => {
    // console.log(e.detail);
    // people.push(e.detail);
    const person = e.detail;
    people = [person, ...people];
    showModal = false;
  };

  let num = 15;
</script>

<Modal isPromo={false} {showModal} on:click={toggleModal}>
  <AddPersonForm on:addPerson={addPerson} />
</Modal>
<main>
  <button on:click={toggleModal}>Open Modal</button>
  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      {#if person.beltColor == "black"}
        <p>Master Ninja</p>
      {/if}
      <p>{person.age} year old, {person.beltColor} belt</p>
      <button on:click={() => handleClick(person.id)}>delete</button>
    </div>
  {:else}
    <p>There are no peopel to show...</p>
  {/each}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
