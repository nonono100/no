## Scripts Overview

<details>
  <summary>RemoteHook</summary>

```lua
local HS = loadstring(game:HttpGet('https://raw.githubusercontent.com/0zBug/HookingService/refs/heads/main/main.lua'))()
  local function HookFunction(originalFunction, remote, ...)
      local args = {...}
      print("arguments:", unpack(args))
      --
      for i = 1, 100 do
          originalFunction(remote, unpack(args))
      end
  
      return originalFunction(remote, unpack(args))
  end
  local remote = workspace
  HS:HookRemote(remote, HookFunction)
```
</details>

---

<details>
  <summary>RemoteFunction spy</summary>

```lua
  local repr = loadstring(game:HttpGet('https://raw.githubusercontent.com/Ozzypig/repr/master/repr.lua'))()
game.StarterGui:SetCore("DevConsoleVisible", true)
```
</details>

---
 
<details>
  <summary>Remote Brute</summary>

```lua
local params = {
    nil, true, false, 0, 1, -1, 100, -100, math.huge, 0/0, "100bucks2", "imadethis12321", workspace, 
    game.Players.LocalPlayer, game.Players.LocalPlayer.Character,
}
for i,v in pairs(game.ReplicatedStorage.Packages:GetDescendants()) do 
    if v:IsA("RemoteEvent") then 
        for i,b in pairs(params) do
            for i,c in pairs(params) do
                pcall(function()
                    v:FireServer(b, c)
                end)
            end
        end
    end
end
```
</details>

---

<details>
  <summary>Extra</summary>

 ```lua
for i,v in pairs(game.ReplicatedStorage:GetDescendants()) do 
    if v:IsA("RemoteEvent") and v.Name ~= "giveMop" and v.Name ~= "ResetPlayerData" and v.Name ~= "Respawn" and not v:IsDescendantOf(game.ReplicatedStorage.spawner) then 
        v:FireServer("Lockpick")
    end
end
```
</details>

---

## ⚠️ Disclaimer  
These scripts are for **educational and security testing purposes only**.
