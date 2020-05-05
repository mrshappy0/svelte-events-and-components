<script>
  import Product from "./Product.svelte";
  import Modal from "./Modal.svelte";

  let showModal = false;
  let closeable = false;

  let products = [{ id: "p1", title: "Art Book", price: 9.99 }];
  function addToCart(event) {
    console.log(event);
  }

  function deleteProduct(bob) {
    console.log(bob);
  }
</script>

{#each products as product}
  <Product {...product} on:add-to-cart={addToCart} on:delete={deleteProduct} />
{/each}

<button on:click={() => (showModal = true)}>Show Modal</button>

{#if showModal}
  <Modal
    on:cancel={() => (showModal = false)}
    on:close={() => (showModal = false)}
    let:didAgree={closeable}>
    <h1 slot="header">"fuck you bob"</h1>
    <p>Yea okay bob!</p>
    <button slot="footer" on:click={() => (showModal = false)} disabled={!closeable}>Confirm</button>
  </Modal>
{/if}
