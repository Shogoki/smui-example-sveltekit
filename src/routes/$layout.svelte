<div style="display: flex; justify-content: space-between;">
  <div class="container"><slot /></div>
  <div class="container">
    <Button on:click={switchTheme}>
      <Label>{lightTheme ? "Lights off" : "Lights on"}</Label>
    </Button>
  </div>
</div>

<script>
  import Button, { Label } from "@smui/button/bare";

  let lightTheme =
    typeof window === "undefined" ||
    window.matchMedia("(prefers-color-scheme: light)").matches;
  function switchTheme() {
    lightTheme = !lightTheme;
    let themeLink = document.head.querySelector("#theme");
    if (!themeLink) {
      themeLink = document.createElement("link");
      themeLink.rel = "stylesheet";
      themeLink.id = "theme";
    }
    themeLink.href = `/smui${lightTheme ? "" : "-dark"}.css`;
    document.head
      .querySelector('link[href="/smui-dark.css"]')
      .insertAdjacentElement("afterend", themeLink);
  }
</script>
