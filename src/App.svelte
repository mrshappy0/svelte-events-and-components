<script>
  import { tick } from "svelte";
  import Product from "./Product.svelte";
  import Modal from "./Modal.svelte";

  let showModal = false;
  let closeable = false;
  let text = "This is some dummy text!";

  let products = [{ id: "p1", title: "Art Book", price: 9.99 }];

  function transformText() {
    if (event.which !== 9) {
      return;
    }
    event.preventDefault();
    const selectionStart = event.target.selectionStart;
    const selectionEnd = event.target.selectionEnd;
    const value = event.target.value;

    text =
      value.slice(0, selectionStart) +
      value.slice(selectionStart, selectionEnd).toUpperCase() +
      value.slice(selectionEnd);
    tick().then(() => {
      event.target.selectionStart = selectionStart;
      event.target.selectionEnd = selectionEnd;
    });
  }

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
    <button
      slot="footer"
      on:click={() => (showModal = false)}
      disabled={!closeable}>
      Confirm
    </button>
  </Modal>
{/if}

<textarea rows="5" value={text} on:keydown={transformText} />
