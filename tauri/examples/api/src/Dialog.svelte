<script>
  import Button, { Label } from '@smui/button';
  import Textfield from '@smui/textfield';
  import Checkbox from '@smui/checkbox';
  import FormField from '@smui/form-field';
  import {
    open,
    save
  } from '@tauri-apps/api/dialog'
  import {
    readBinaryFile
  } from '@tauri-apps/api/fs'

  export let onMessage
  let defaultPath = ''
  let filter = ''
  let multiple = false
  let directory = false

  function arrayBufferToBase64(buffer, callback) {
    var blob = new Blob([buffer], {
      type: "application/octet-binary",
    });
    var reader = new FileReader();
    reader.onload = function (evt) {
      var dataurl = evt.target.result;
      callback(dataurl.substr(dataurl.indexOf(",") + 1));
    };
    reader.readAsDataURL(blob);
  }

  function openDialog() {
    open({
      defaultPath,
      filters: filter ? [{
        name: 'Tauri Example',
        extensions: filter.split(',').map(f => f.trim())
      }] : [],
      multiple,
      directory
    }).then(function (res) {
      if (Array.isArray(res)) {
        onMessage(res)
      } else {
        var pathToRead = res
        var isFile = pathToRead.match(/\S+\.\S+$/g)
        readBinaryFile(pathToRead).then(function (response) {
          if (isFile) {
            if (pathToRead.includes('.png') || pathToRead.includes('.jpg')) {
              arrayBufferToBase64(new Uint8Array(response), function (base64) {
                var src = 'data:image/png;base64,' + base64
                onMessage('<img src="' + src + '"></img>')
              })
            } else {
              onMessage(res)
            }
          } else {
            onMessage(res)
          }
        }).catch(onMessage(res))
      }
    }).catch(onMessage)
  }

  function saveDialog() {
    save({
      defaultPath,
      filters: filter ? [{
        name: 'Tauri Example',
        extensions: filter.split(',').map(f => f.trim())
      }] : [],
    }).then(onMessage).catch(onMessage)
  }

</script>

<style>
  #dialog-filter {
    width: 260px;
  }
</style>

<div style="margin-top: 24px">
  <Textfield label="Default path" bind:value={defaultPath}></Textfield>
  <Textfield id="dialog-filter" label="Filter" placeholder="Extensions filter, comma-separated" bind:value={filter}>
  </Textfield>
  <div>
    <FormField>
      <Checkbox bind:checked={multiple} />
      <span slot="label">Multiple</span>
    </FormField>
  </div>
  <div>
    <FormField>
      <Checkbox bind:checked={directory} />
      <span slot="label">Directory</span>
    </FormField>
  </div>

  <Button variant="raised" on:click={openDialog}>
    <Label>Open dialog</Label>
  </Button>
  <Button variant="raised" on:click={saveDialog}>
    <Label>Open save dialog</Label>
  </Button>
</div>