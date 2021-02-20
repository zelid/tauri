<script>
  import Button, { Label } from '@smui/button';
  import Select, { Option } from '@smui/select';
  import Textfield from '@smui/textfield';
  import { getClient, Body } from "@tauri-apps/api/http";
  let httpMethod = "GET";
  let httpUrl = "";
  let httpBody = "";

  export let onMessage;

  async function makeHttpRequest() {
    const client = await getClient()
    let method = httpMethod || "GET";
    let url = httpUrl || "";

    const options = {
      url: url || "",
      method: method || "GET"
    };

    if (
      (httpBody.startsWith("{") && httpBody.endsWith("}")) ||
      (httpBody.startsWith("[") && httpBody.endsWith("]"))
    ) {
      options.body = Body.json(JSON.parse(httpBody));
    } else if (httpBody !== '') {
      options.body = Body.text(httpBody)
    }

    client.request(options)
      .then(onMessage)
      .catch(onMessage);
  }
</script>

<form id="http" on:submit|preventDefault={makeHttpRequest}>
  <Select bind:value={httpMethod}>
    <Option value="GET">GET</Option>
    <Option value="POST">POST</Option>
    <Option value="PUT">PUT</Option>
    <Option value="PATCH">PATCH</Option>
    <Option value="DELETE">DELETE</Option>
  </Select>
  <Textfield label="URL" placeholder="Type the request URL..." bind:value={httpUrl}></Textfield>
  <br />
  <Textfield textarea label="Body" placeholder="Request body" rows="5"
    style="width:100%;margin-right:10px;font-size:12px" bind:value={httpBody}></Textfield>
  <Button variant="raised" for="http" type="submit">
    <Label>Make request</Label>
  </Button>
</form>