<script lang="ts">
  import MyButton from "./button.svelte";
  import MyDialog from "./dialog.svelte";

  let showValidDialog = false;
  let showInvalidDialog = false;

  const openValidDialog = () => {
    showValidDialog = true;
  };

  const openInvalidDialog = () => {
    showInvalidDialog = true;
  };

  const handleAccept = () => {
    console.log("Dialog accepted!");
    showValidDialog = false;
  };

  const handleAcceptInvalid = () => {
    console.log("Invalid dialog accepted!");
    showInvalidDialog = false;
  };
</script>

<main>
  <h1>Component Type Validation Demo</h1>

  <div class="demo-section">
    <h2>Valid Dialog (uses My-Button)</h2>
    <MyButton
      label="Open Valid Dialog"
      variant="primary"
      onclick={openValidDialog}
    />

    <MyDialog bind:open={showValidDialog} title="Valid Dialog">
      {#snippet children()}
        <p>
          This dialog uses only My-Button components and should work without
          errors.
        </p>
      {/snippet}
      {#snippet acceptButton()}
        <MyButton label="Accept" variant="primary" onclick={handleAccept} />
        <MyButton
          label="Cancel"
          variant="secondary"
          onclick={() => (showValidDialog = false)}
        />
      {/snippet}
    </MyDialog>
  </div>

  <div class="demo-section">
    <h2>Invalid Dialog (uses HTML button)</h2>
    <MyButton
      label="Open Invalid Dialog"
      variant="secondary"
      onclick={openInvalidDialog}
    />

    <MyDialog bind:open={showInvalidDialog} title="Invalid Dialog">
      {#snippet children()}
        <p>
          This dialog uses an HTML button element and should show an error in
          the console.
        </p>
      {/snippet}
      {#snippet acceptButton()}
        <!-- This will trigger validation error -->
        <button class="invalid-button" onclick={handleAcceptInvalid}
          >Invalid Button</button
        >
        <MyButton
          label="Cancel"
          variant="secondary"
          onclick={() => (showInvalidDialog = false)}
        />
      {/snippet}
    </MyDialog>
  </div>
</main>

<style>
  main {
    padding: 2rem;
    max-width: 800px;
    margin: 0 auto;
  }

  h1 {
    color: #333;
    text-align: center;
    margin-bottom: 2rem;
  }

  .demo-section {
    margin-bottom: 2rem;
    padding: 1rem;
    border: 1px solid #e5e7eb;
    border-radius: 8px;
  }

  .demo-section h2 {
    color: #374151;
    margin-bottom: 1rem;
  }

  .invalid-button {
    padding: 8px 16px;
    background-color: #ef4444;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    margin-right: 8px;
  }
</style>
