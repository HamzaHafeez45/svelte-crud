<script>

    import { onMount } from 'svelte';
    import axios from 'axios';
    let categories = [];
    let category="";
    let joke = {};
    let error = null;


    const getRandom= async ()=>{
        try {
            const response = await axios.get(`https://api.chucknorris.io/jokes/random`);
            joke = response.data;
        } catch (e) {
            error = e;
            console.log(error);
        }
	}

    const getAllCategories= async ()=>{
		try {
            const response = await axios.get(`https://api.chucknorris.io/jokes/categories`);
            categories=response.data;
        } catch (e) {
            error = e;
            console.log(error);
        }
	}
    const onChange = async () => {
		try {
            const response = await axios.get(`https://api.chucknorris.io/jokes/random?category=${category}`);
            joke=response.data;
        } catch (e) {
            error = e;
            console.log(error);
        }
	}

    onMount(() => {
        getAllCategories();
        getRandom();
    });


</script>

<div class="main-container">
    <div class="heading">
        <h1 class="heading__title">Chuck Api Integeration</h1>
        <!-- <input type="search" id="gsearch" name="gsearch">
        <input type="submit"> -->
        <br/>
        <label for="categories">Select Category</label><br/>
        <select name="categories"  bind:value={category} on:change={onChange}>
            {#each categories as category, index (index)}
            
                <option value={category} key={index}>{category}</option>
            {/each}
        </select>
    </div>
    <div class="cards">
      <div class="card" key={joke?.id}>
        <h2 class="card__title">{joke?.value ? joke?.value : "Loading..."}</h2>
      </div>
    </div>
  </div>

  <style>
    select {
		width: 30%;
		padding: 12px 20px;
		margin: 8px 0;
		display: inline-block;
		border: 2px solid #ccc;
		border-radius: 4px;
		box-sizing: border-box;
	}

.main-container {
  padding: 30px;
}

/* HEADING */

.heading {
  text-align: center;
}

.heading__title {
  font-weight: 600;
}


/* CARDS */

.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.card {
  margin: 20px;
  padding: 20px;
  width: 500px;
  min-height: 200px;
  display: grid;
  grid-template-rows: 20px 50px 1fr 50px;
  border-radius: 10px;
  background: radial-gradient(#1fe4f5, #3fbafe);
}
.card__title {
    grid-row: 3/4;
    font-weight: 400;
    color: #ffffff;
}

/* RESPONSIVE */

@media (max-width: 1600px) {
  .cards {
    justify-content: center;
  }
}

  </style>