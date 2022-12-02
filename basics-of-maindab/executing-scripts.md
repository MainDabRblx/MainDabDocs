---
description: This part is simple too, but it's here just in case.
---

# Executing Scripts

### Quick note

Please make sure you have gone though [the UI basics](maindabs-ui.md). If you have not, it is recommended you do.\
\
Now that you've gone over the UI basics and you now wish to just go on and use MainDab. Hopefully you've remembered what you saw (you can always go back and look again), and you're ready to start exploiting.

{% hint style="info" %}
If you have questions on this, join MainDab's Discord at [https://discord.io/maindab](https://discord.io/maindab)
{% endhint %}

### Great, let's get started...

Hopefully you remembered what you saw in UI basics. Here are the numbered steps for injection and execution.

1. Select a DLL/API, according to the API status
2. Press the inject icon
3. Wait for injection to finish
4. Paste in the intended script into the textbox you wish to run
5. Press the execute button

And that's all! The script should be executed.

Confused? You shouldn't be, as this is pretty straight forward. However, below are step by step instructions on how to do so.

### Step 1: API selection

You might have noticed that in MainDab's execution tab, there is a label on the bottom right telling you which API is selected. That's the API that is selected, and you can select what API to use from the settings tab.

#### What's the point of selecting different APIs?

As of time of writing, MainDab only has three APIs : EasyExploits, Oxygen U and WeAreDevs. All three APIs have different execution power. For example, EasyExploits may support a script that WeAreDevs clearly doesn't.\
\
More importantly, Roblox updates every **Wednesday/Thursday**. Exploits are then outdated, in which the APIs (exploits) take usually around a few hours to update again.

#### How do I select an API then?

Go to the settings tab to find the API selection. The coloured circles tell you whether the API is updated or not, and the text below the API name will also tell you. In order to select an API, simply click "Use".

![Red - Not updated, Orange - No way to check, Green - Updated (MainDab 14.9)](../.gitbook/assets/MainDab\_R1Tq00vEkZ.png)

### Step 2-5: Actually exploiting

{% hint style="warning" %}
If the APIs are not yet updated, they will crash Roblox, and you can get a 1 hour temporary HWID ban. Roblox updates every Wednesday, meaning you have to wait for the API to update.
{% endhint %}

Let's assume that all the APIs are working. For our example, we will be using EasyExploits API. However, WeAreDevs API has actually signifiantly improved since 2021.

The first step to using MainDab is to inject MainDab into Roblox.

**First, you must open Roblox.** Exploits can't inject out of nowhere. You can check and see whether you are ready to inject by checking the status on the bottom left of the execution page.

![The status and API that you're using (MainDab 14.9)](../.gitbook/assets/MainDab\_gjwW1sbttf.png)

Next, once Roblox is open, inject into Roblox. If you already forgot, click the Syringe button to inject into Roblox. **You must open Roblox first.**

![You can see that WeAreDevs is now injected. (MainDab 14.9)](../.gitbook/assets/RobloxPlayerBeta\_4Jq68ANZoy.png)

{% hint style="warning" %}
If Roblox crashes or some random error pops up, that means the API isn't updated. Or you might just have to reinject MainDab.
{% endhint %}

#### Execution

Now, let's press the execute button. If you already forgot (yet again), it's the play button.\
\
Press F9 to open the developer console, and it should print `MainDab Funnies :3`

![ I spammed the execute button for your own reference... (MainDab 14.9)](../.gitbook/assets/RobloxPlayerBeta\_dWfSVlqt5b.gif)

Now, let's try this generic fly script. Try copy the script from below :

{% code overflow="wrap" lineNumbers="true" %}
```lua
-- Press "E" to fly.

repeat wait()
   until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("Torso") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid")
local mouse = game.Players.LocalPlayer:GetMouse()
repeat wait() until mouse
local plr = game.Players.LocalPlayer
local torso = plr.Character.Torso
local flying = true
local deb = true
local ctrl = {f = 0, b = 0, l = 0, r = 0}
local lastctrl = {f = 0, b = 0, l = 0, r = 0}
local maxspeed = 50
local speed = 0

function Fly()
local bg = Instance.new("BodyGyro", torso)
bg.P = 9e4
bg.maxTorque = Vector3.new(9e9, 9e9, 9e9)
bg.cframe = torso.CFrame
local bv = Instance.new("BodyVelocity", torso)
bv.velocity = Vector3.new(0,0.1,0)
bv.maxForce = Vector3.new(9e9, 9e9, 9e9)
repeat wait()
plr.Character.Humanoid.PlatformStand = true
if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then
speed = speed+.5+(speed/maxspeed)
if speed > maxspeed then
speed = maxspeed
end
elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then
speed = speed-1
if speed < 0 then
speed = 0
end
end
if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r}
elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
else
bv.velocity = Vector3.new(0,0.1,0)
end
bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0)
until not flying
ctrl = {f = 0, b = 0, l = 0, r = 0}
lastctrl = {f = 0, b = 0, l = 0, r = 0}
speed = 0
bg:Destroy()
bv:Destroy()
plr.Character.Humanoid.PlatformStand = false
end
mouse.KeyDown:connect(function(key)
if key:lower() == "e" then
if flying then flying = false
else
flying = true
Fly()
end
elseif key:lower() == "w" then
ctrl.f = 1
elseif key:lower() == "s" then
ctrl.b = -1
elseif key:lower() == "a" then
ctrl.l = -1
elseif key:lower() == "d" then
ctrl.r = 1
end
end)
mouse.KeyUp:connect(function(key)
if key:lower() == "w" then
ctrl.f = 0
elseif key:lower() == "s" then
ctrl.b = 0
elseif key:lower() == "a" then
ctrl.l = 0
elseif key:lower() == "d" then
ctrl.r = 0
end
end)
Fly()
```
{% endcode %}

And paste the script into MainDab. Click execute, and watch the script work.

![This is how it looks like! (MainDab 14.9)](../.gitbook/assets/RobloxPlayerBeta\_1qvdU4NpHx.gif)

**Congratulations!** You successfully used MainDab. If this is your first time exploiting, you probably aren't that stupid and made it here...

But... where do I find scripts for games?
