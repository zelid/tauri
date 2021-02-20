<script>
  import Button, { Label } from '@smui/button';
  import { getMatches } from "@tauri-apps/api/cli";

  export let onMessage;

  function cliMatches() {
    getMatches()
      .then(onMessage)
      .catch(onMessage);
  }
</script>

<div style="margin-top: 24px">
  <Button variant="raised" on:click={cliMatches}>
    <Label>Get matches</Label>
  </Button>
</div>