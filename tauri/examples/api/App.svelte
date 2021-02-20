<script>
  import Tab, { Icon, Label } from '@smui/tab';
  import TabBar from '@smui/tab-bar';
  import { onMount } from "svelte";
  import { open } from "@tauri-apps/api/window"

  import Cli from './src/Cli.svelte'
  import Communication from './src/Communication.svelte'
  import Dialog from './src/Dialog.svelte'
  import FileSystem from './src/FileSystem.svelte'
  import Http from './src/Http.svelte'
  import Notifications from './src/Notifications.svelte'
  import Window from './src/Window.svelte'
  import Shortcuts from './src/Shortcuts.svelte'

  const views = [{
    label: 'Messages',
    component: Communication
  }, {
    label: 'CLI',
    component: Cli
  }, {
    label: 'Dialog',
    component: Dialog
  }, {
    label: 'File system',
    component: FileSystem
  }, {
    label: 'HTTP',
    component: Http
  }, {
    label: 'Notifications',
    component: Notifications
  }, {
    label: 'Window',
    component: Window
  }, {
    label: 'Shortcuts',
    component: Shortcuts
  }]

  let selected = views[0];

  let response = '';
  let currentView

  function onMessage(value) {
    response = typeof value === "string" ? value : JSON.stringify(value);
  }

  function onLogoClick() {
    open("https://tauri.studio/");
  }

  $: currentView = selected.component
</script>

<style>
  .logo-container {
    width: 95%;
    margin: 0px auto;
    overflow: hidden;
  }

  .logo-link {
    font-weight: 700;
    position: absolute;
    top: 150px;
    right: 10px;
  }

  .logo {
    width: 32px;
    height: 32px;
    cursor: pointer;
    position: fixed;
    z-index: 10;
    top: 7px;
    right: 10px;
  }

  #response {
    position: absolute;
    left: 10px;
    right: 10px;
    top: 440px;
    min-height: 110px;
    background: #aab;
    font-family: "Courier New", Courier, monospace;
    font-size: 12px;
    word-wrap: break-word;
    padding: 5px;
    border-radius: 5px;
    overflow-y: auto;
  }
</style>

<main>
  <div class="logo-container">
    <img src="icon.png" class="logo" on:click={onLogoClick} alt="logo" />
  </div>

  <div class="tabs-container">
    <TabBar tabs={views} let:tab key={tab=> tab.label} bind:active={selected}>
      <Tab {tab} tabIndicator$transition="fade">
        <Label>{tab.label}</Label>
      </Tab>
    </TabBar>
  </div>
  <svelte:component this={currentView} {onMessage} />

  <div id="response">{@html response}</div>
  <div class="bottom">
    <a class="dark-link" target="_blank" href="https://tauri.studio">
      Tauri Documentation
    </a>
    &nbsp;&nbsp;&nbsp;
    <a class="dark-link" target="_blank" href="https://github.com/tauri-apps/tauri">
      Github Repo
    </a>
    &nbsp;&nbsp;&nbsp;
    <a class="dark-link" target="_blank" href="https://github.com/tauri-apps/tauri/tree/dev/tauri/examples/api">
      Source for this App
    </a>
  </div>
</main>