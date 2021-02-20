<script>
  import Button, { Label } from '@smui/button';
  import Textfield from '@smui/textfield';
  import Checkbox from '@smui/checkbox';
  import FormField from '@smui/form-field';
  import { manager as windowManager } from "@tauri-apps/api/window";
  import { open as openDialog } from '@tauri-apps/api/dialog'
  import { open } from "@tauri-apps/api/shell";

  const {
    setResizable,
    setTitle,
    maximize,
    unmaximize,
    minimize,
    unminimize,
    show,
    hide,
    setTransparent,
    setDecorations,
    setAlwaysOnTop,
    setWidth,
    setHeight,
    // resize,
    setMinSize,
    setMaxSize,
    setX,
    setY,
    // setPosition,
    setFullscreen,
    setIcon
  } = windowManager

  let urlValue = "https://tauri.studio";
  let resizable = true
  let maximized = false
  let transparent = false
  let decorations = false
  let alwaysOnTop = false
  let fullscreen = false
  let width = 600
  let height = 600
  let minWidth = 600
  let minHeight = 600
  let maxWidth = 0
  let maxHeight = 0
  let x = 300
  let y = 300

  let windowTitle = 'Awesome Tauri Example!';

  function openUrl() {
    open(urlValue);
  }

  function setTitle_() {
    setTitle(windowTitle);
  }

  function hide_() {
    hide()
    setTimeout(show, 2000)
  }

  function minimize_() {
    minimize()
    setTimeout(unminimize, 2000)
  }

  function getIcon() {
    openDialog({
      multiple: false
    }).then(setIcon)
  }

  $: setResizable(resizable)
  $: maximized ? maximize() : unmaximize()
  $: setTransparent(transparent)
  $: setDecorations(decorations)
  $: setAlwaysOnTop(alwaysOnTop)
  $: setFullscreen(fullscreen)

  $: setWidth(width)
  $: setHeight(height)
  $: minWidth && minHeight && setMinSize(minWidth, minHeight)
  $: maxWidth && maxHeight && setMaxSize(maxWidth, maxHeight)
  $: setX(x)
  $: setY(y)
</script>

<style>
  .flex {
    display: flex;
  }

  .flex-row {
    flex-direction: row;
  }

  .flex-column {
    flex-direction: column;
  }

  .grow {
    flex-grow: 1;
  }

  .window-controls Textfield {
    width: 50px;
  }
</style>

<div class="flex flex-column">
  <div>
    <FormField>
      <Checkbox bind:checked={resizable} />
      <span slot="label">Resizable</span>
    </FormField>
    <FormField>
      <Checkbox bind:checked={maximized} />
      <span slot="label">Maximize</span>
    </FormField>
    <Button variant="raised" title="Unminimizes after 2 seconds" on:click={minimize_}>
      Minimize
    </Button>
    <Button variant="raised" title="Visible again after 2 seconds" on:click={hide_}>
      Hide
    </Button>
    <FormField>
      <Checkbox bind:checked={transparent} />
      <span slot="label">Transparent</span>
    </FormField>
    <FormField>
      <Checkbox bind:checked={decorations} />
      <span slot="label">Has decorations</span>
    </FormField>
    <FormField>
      <Checkbox bind:checked={alwaysOnTop} />
      <span slot="label">Always on top</span>
    </FormField>
    <FormField>
      <Checkbox bind:checked={fullscreen} />
      <span slot="label">Fullscreen</span>
    </FormField>
    <Button variant="raised" on:click={getIcon}>
      Change icon
    </Button>
  </div>
  <div>
    <div class="window-controls flex flex-row">
      <div class="flex flex-column grow">
        <div>
          <Textfield label="X" type="number" bind:value={x} input$min="0"></Textfield>
        </div>
        <div>
          <Textfield label="Y" type="number" bind:value={y} input$min="0"></Textfield>
        </div>
      </div>

      <div class="flex flex-column grow">
        <div>
          <Textfield label="Width" type="number" bind:value={width} input$min="400"></Textfield>
        </div>
        <div>
          <Textfield label="Height" type="number" bind:value={height} input$min="400"></Textfield>
        </div>
      </div>

      <div class="flex flex-column grow">
        <div>
          <Textfield label="Min width" type="number" bind:value={minWidth}></Textfield>
        </div>
        <div>
          <Textfield label="Min height" type="number" bind:value={minHeight}></Textfield>
        </div>
      </div>

      <div class="flex flex-column grow">
        <div>
          <Textfield label="Max width" type="number" bind:value={maxWidth} input$min="400"></Textfield>
        </div>
        <div>
          <Textfield label="Max height" type="number" bind:value={maxHeight} input$min="400"></Textfield>
        </div>
      </div>
    </div>
  </div>
</div>
<form id="set-title" style="margin-top: 24px" on:submit|preventDefault={setTitle_}>
  <Textfield bind:value={windowTitle}></Textfield>
  <Button variant="raised" for="set-title" type="submit">
    <Label>Set title</Label>
  </Button>
</form>
<form id="open-url" style="margin-top: 24px" on:submit|preventDefault={openUrl}>
  <Textfield bind:value={urlValue}></Textfield>
  <Button variant="raised" for="open-url" type="submit">
    <Label>Open URL</Label>
  </Button>
</form>