<script>
  import Button, { Label } from '@smui/button';
  export let onMessage;

  function _sendNotification() {
    new Notification("Notification title", {
      body: "This is the notification body"
    });
  }

  function sendNotification() {
    if (Notification.permission === "default") {
      Notification.requestPermission()
        .then(function (response) {
          if (response === "granted") {
            _sendNotification();
          } else {
            onMessage("Permission is " + response);
          }
        })
        .catch(onMessage);
    } else if (Notification.permission === "granted") {
      _sendNotification();
    } else {
      onMessage("Permission is denied");
    }
  }
</script>

<Button variant="raised" on:click={sendNotification}>
  <Label>Send test notification</Label>
</Button>