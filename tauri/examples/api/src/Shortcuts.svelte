<script>
  import Button, { Label } from '@smui/button';
  import Textfield from '@smui/textfield';
  import { writable } from 'svelte/store'
  import {
    register as registerShortcut,
    unregister as unregisterShortcut,
    unregisterAll as unregisterAllShortcuts
  } from '@tauri-apps/api/globalShortcut'

  export let onMessage
  const shortcuts = writable([])
  let shortcut = 'CmdOrControl+X'

  function register() {
    const shortcut_ = shortcut
    registerShortcut(shortcut_, () => {
      onMessage(`Shortcut ${shortcut_} triggered`)
    }).then(() => {
      shortcuts.update(shortcuts_ => [...shortcuts_, shortcut_])
      onMessage(`Shortcut ${shortcut_} registered successfully`)
    }).catch(onMessage)
  }

  function unregister(shortcut) {
    const shortcut_ = shortcut
    unregisterShortcut(shortcut_).then(() => {
      shortcuts.update(shortcuts_ => shortcuts_.filter(s => s !== shortcut_))
      onMessage(`Shortcut ${shortcut_} unregistered`)
    }).catch(onMessage)
  }

  function unregisterAll() {
    unregisterAllShortcuts().then(() => {
      shortcuts.update(() => [])
      onMessage(`Unregistered all shortcuts`)
    }).catch(onMessage)
  }
</script>

<div style="margin-top: 24px">
  <div>
    <Textfield label="Shortcut" placeholder="Type a shortcut with '+' as separator..." bind:value={shortcut}>
    </Textfield>
    <Button variant="raised" on:click={register}>Register</Button>
  </div>
  <div>
    {#each $shortcuts as savedShortcut}
    <div>
      {savedShortcut}
      <Button variant="raised" on:click={()=> unregister(savedShortcut)}>Unregister</Button>
    </div>
    {/each}
    {#if $shortcuts.length}
    <Button variant="raised" on:click={unregisterAll}>Unregister all</Button>
    {/if}
  </div>
</div>