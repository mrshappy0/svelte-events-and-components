<script>
  import { createEventDispatcher } from "svelte";
  export let title;
  export let price;
  export let id;
  export let bestseller = false;


  const dispatch = createEventDispatcher();

  function addToCart(){
      dispatch('add-to-cart', {id: 'p1'})
  }
</script>

<article id={id}>
  <h1>{title}</h1>
  <h2>${price}</h2>
  <p>{bestseller}</p>
  <button on:click="{addToCart}">Add to Cart</button>
  <button on:click={()=>{dispatch('delete', 'p1')}}>Delete</button>
</article>
