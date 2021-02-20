<script>
  import Button, { Label } from '@smui/button';
  import Select, { Option } from '@smui/select';
  import Textfield from '@smui/textfield';
  import {
    readBinaryFile,
    readDir,
    Dir,
  } from '@tauri-apps/api/fs'

  export let onMessage

  const DirOptions = Object.keys(Dir)
    .filter(key => isNaN(parseInt(key)))
    .map(dir => [dir, Dir[dir]]);

  let pathToRead = ''
  let dir = ''

  function arrayBufferToBase64(buffer, callback) {
    const blob = new Blob([buffer], {
      type: 'application/octet-binary'
    })
    const reader = new FileReader()
    reader.onload = function (evt) {
      const dataurl = evt.target.result
      callback(dataurl.substr(dataurl.indexOf(',') + 1))
    }
    reader.readAsDataURL(blob)
  }

  function read() {
    const isFile = pathToRead.match(/\S+\.\S+$/g)
    const opts = {
      dir: parseInt(dir || 0)
    }
    const promise = isFile ? readBinaryFile(pathToRead, opts) : readDir(pathToRead, opts)
    promise.then(function (response) {
      if (isFile) {
        if (pathToRead.includes('.png') || pathToRead.includes('.jpg')) {
          arrayBufferToBase64(new Uint8Array(response), function (base64) {
            const src = 'data:image/png;base64,' + base64
            onMessage('<img src="' + src + '"></img>')
          })
        } else {
          const value = String.fromCharCode.apply(null, response)
          onMessage('<textarea id="file-response" style="height: 400px"></textarea><Button variant="raised"id="file-save">Save</button>')
          setTimeout(() => {
            const fileInput = document.getElementById('file-response')
            fileInput.value = value
            document.getElementById('file-save').addEventListener('click', function () {
              writeFile({
                file: pathToRead,
                contents: fileInput.value
              }, {
                dir: parseInt(dir || 0)
              }).catch(onMessage)
            })
          })
        }
      } else {
        onMessage(response)
      }
    }).catch(onMessage)
  }
</script>

<form id="fs" style="margin-top: 24px" on:submit|preventDefault={read}>
  <Select bind:value={dir} label="Base dir">
    <Option value="">None</Option>
    {#each DirOptions as dir}
    <Option value={dir[1]}>{dir[0]}</Option>
    {/each}
  </Select>
  <Textfield label="Path" placeholder="Type the path to read..." bind:value={pathToRead}></Textfield>
  <Button variant="raised" for="fs" type="submit">
    <Label>Read</Label>
  </Button>
</form>