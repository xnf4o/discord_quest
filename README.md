## Complete Recent Discord Quest
> [!NOTE]
> This no longer works in browser!

> [!NOTE]
> This no longer works if you're alone in vc! Somebody else has to join you!

How to use this script:
1. Accept the quest under User Settings -> Gift Inventory
2. Join a vc
3. **Join the same vc on an alt**
4. Stream any window (can be notepad or something)
5. Press <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>I</kbd> to open DevTools
6. Go to the `Console` tab
7. Paste the following code and hit enter:
> [!NOTE]
> if you can't paste your code in console then type in console `allow pasting`!
```js
let wpRequire;
window.webpackChunkdiscord_app.push([[Math.random()],{},req=>wpRequire=req]);
let a=Object.values(wpRequire.c).find(x=>x?.exports?.getAPIBaseURL)?.exports.HTTP,
    A=Object.values(wpRequire.c).find(x=>x?.exports?.default?.getStreamerActiveStreamMetadata)?.exports.default,
    Q=Object.values(wpRequire.c).find(x=>x?.exports?.default?.getQuest)?.exports.default,
    e=Object.values(wpRequire.c).find(x=>x?.exports?.encodeStreamKey)?.exports.encodeStreamKey,
    sl=(ms)=>new Promise(resolve=>setTimeout(resolve,ms));
let i=navigator.userAgent.includes("Electron/"),
    q=[...Q.quests.values()].find(x=>x.userStatus?.enrolledAt&&!x.userStatus?.completedAt&&new Date(x.config.expiresAt).getTime()>Date.now());
if(!i){
  console.log("[EN-US] This no longer works in browser. Use the desktop app!");
} else if (!q) {
  console.log("[EN-US] You don't have any incomplete quests!");
  console.log("[RU] У вас нет незавершенных квестов!");
} else {
  let s=e(A.getCurrentUserActiveStream()),
      t=q.config.streamDurationRequirementMinutes*60;
  async function h(){
    console.log("[EN-US] Starting quest:",q.config.messages.gameTitle,"-",q.config.messages.questName);
    console.log("[RU] Начинается квест:",q.config.messages.gameTitle,"-",q.config.messages.questName);
    while(true){
      let r=await a.post({url:`/quests/${q.id}/heartbeat`,body:{stream_key:s}});
      let p=r.body.stream_progress_seconds;
      console.log(`[EN-US] Quest progress: ${p}/${t}`);
      console.log(`[RU] Прогресс квеста: ${p}/${t}`);
      if(p>=t)break;
      await sl(30*1000);
    }
    console.log("[EN-US] Quest completed!");
    console.log("[RU] Квест завершен!");
  }
  h();
}
```
7. Keep the stream running for 15 minutes
8. You can now claim the reward in User Settings -> Gift Inventory!

You can track the progress by looking at the `Quest progress:` prints in the Console tab, or by reopening the Gift Inventory tab in settings. The progress should update every 30s.

## FAQ

**Q: Ctrl + Shift + I doesn't work**

A: Either download the [ptb client](https://discord.com/api/downloads/distributions/app/installers/latest?channel=ptb&platform=win&arch=x64), or use [this](https://www.reddit.com/r/discordapp/comments/sc61n3/comment/hu4fw5x/) to enable DevTools on stable


**Q: I get an error saying "Unauthorized"**

A: Discord has patched the script from working in browsers. Use the desktop app, or alternatively find some extension which lets you change your User-Agent and append the string `Electron/` anywhere in it.

They have also started checking how many people are in the vc, so make sure you join it on at least 1 other account.


**Q: I get a different error**

A: Make sure you're copy/pasting the script correctly and that you've have done all the steps.
