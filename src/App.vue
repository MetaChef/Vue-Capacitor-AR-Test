<template>
  <button
    @click="
      launchAR(
        'intent://arvr.google.com/scene-viewer/1.0?file=https://cdn.metachef.app/dev/ar_test.glb&mode=ar_only#Intent;scheme=https;package=com.google.ar.core;action=android.intent.action.VIEW;S.browser_fallback_url=https://developers.google.com/ar;end;'
      )
    "
  >
    Open AR (button)
  </button>
</template>

<script>
import { Capacitor, registerPlugin } from "@capacitor/core";
import { NativeARViewer } from "native-ar-viewer";

const ARIntentPlugin = registerPlugin("ARIntentPlugin");

export default {
  name: "MyComponent",
  methods: {
    async launchAR(intentUrl) {
      if (Capacitor.getPlatform() === "android") {
        try {
          await NativeARViewer.openAR({ intent: intentUrl });
          console.log("AR Intent launched");
        } catch (e) {
          console.error("Error launching AR", e);
        }
      } else if (Capacitor.getPlatform() === "ios") {
        try {
          await Browser.open({ url: 'https://cdn.metachef.app/dev/ar_test.usdz', presentationStyle: 'popover'});
          console.log("AR browser launched");
        } catch (e) {
          console.error("Error launching AR", e);
        }
      }
    },
  },
};
</script>
