<script>
  import Button, { Label } from '@smui/button';
  import { listen, emit } from "@tauri-apps/api/event";
  import { invoke } from "@tauri-apps/api/tauri";

  export let onMessage

  listen("rust-event", onMessage);

  function log() {
    invoke({
      cmd: "logOperation",
      event: "tauri-click",
      payload: "this payload is optional because we used Option in Rust"
    });
  }

  function performRequest() {
    invoke({
      cmd: "performRequest",
      endpoint: "dummy endpoint arg",
      body: {
        id: 5,
        name: "test"
      }
    })
      .then(onMessage)
      .catch(onMessage);
  }

  function emitEvent() {
    emit("js-event", "this is the payload string");
  }
</script>

<div>
  <Button variant="raised" on:click={log}>
    <Label>Call Log API</Label>
  </Button>
  <Button variant="raised" on:click={performRequest}>
    <Label>Call Request (async) API</Label>
  </Button>
  <Button variant="raised" on:click={emitEvent}>
    <Label>Send event to Rust</Label>
  </Button>
</div>