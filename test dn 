
-- CONFIG & LIBS
local SECRET_TOKEN = "5PloBkNbTn4zV8YLjsVJVNweS1J2LbwU"

local function getSecureURL(path)   
    if string.sub(path, 1, 5) == "json/" or string.sub(path, 1, 8) == "scripts/" or string.sub(path, 1, 10) == "animation/" then
        return "https://storage.dimszyhub.my.id/" .. path .. "?token=" .. SECRET_TOKEN
    end
 return "https://raw.githubusercontent.com/udineak48-gif/Main/refs/heads/main/" .. path
end 

local JsonCache = {} 
local ROOT_MOUNT_PATH = "BALABALA/mount_data/" 

local function getInternalMountPath(mountBaseName, file)
    return ROOT_MOUNT_PATH .. mountBaseName .. "/" .. file
end

-- Fungsi untuk memastikan Folder Mount sudah dibuat
local function ensureMountFolders(mountBaseName)
    local fullPath = ROOT_MOUNT_PATH .. mountBaseName
    if isfolder and makefolder then
        if not isfolder(fullPath) then 
            local ok, err = pcall(makefolder, fullPath)
            if not ok then
                warn("[Auto Walk] GAGAL membuat folder mount: " .. tostring(err) .. " | Path: " .. fullPath)
            end
        end
    else
        warn("[Auto Walk] Fungsi isfolder atau makefolder tidak tersedia!")
    end
end


local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local HttpService = game:GetService("HttpService")
local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local VirtualUser = game:GetService("VirtualUser")
local MarketplaceService = game:GetService("MarketplaceService")
local TeleportService = game:GetService("TeleportService")
local Debris = game:GetService("Debris")
local player = Players.LocalPlayer
local placeId = game.PlaceId
local jobId = game.JobId
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:FindFirstChildOfClass("Humanoid") or character:WaitForChild("Humanoid")
local humanoidRootPart = character:FindFirstChild("HumanoidRootPart") or character:WaitForChild("HumanoidRootPart")



local DimszyHUB16
do
    local ok, result = pcall(function()
        return require("./src/Init")
    end)
    
    if ok then
        DimszyHUB16 = result
    else 
        DimszyHUB16 = loadstring(game:HttpGet("https://raw.githubusercontent.com/Footagesus/WindUI/main/dist/main.lua"))()
    end
end


-- Create window
DimszyHUB16:SetTheme("Crimson")
local Window = DimszyHUB16:CreateWindow({
Title = "FREE SCRIPTS BYE DN SCRIPTS| Auto Walk",
Author = "Join Discord: dsc.gg/namadiscorlu",
    Icon = "navigation",
    NewElements = true,
    Theme = "Crimson",
	Background = "rbxassetid://113251751851003",
    User = {
        Enabled = true,
        Anonymous = true,
        Callback = function(WindowUI)
            
            if WindowUI and WindowUI:FindFirstChild("UserContainer") then
                local container = WindowUI:FindFirstChild("UserContainer")
                local nameLabel = container:FindFirstChild("Username") 
                    or container:FindFirstChild("Name") 
                    or container:FindFirstChildWhichIsA("TextLabel")
                if nameLabel then
                    nameLabel.Text = "@" .. player.Name
                end
            end
        end,
    },
    OpenButton = {
       Title = "FREE SCRIPTS",
    Icon = "",
    CornerRadius = UDim.new(0, 10),
    StrokeThickness = 2.2,
    Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(120, 0, 0)),
        ColorSequenceKeypoint.new(0.5, Color3.fromRGB(180, 20, 20)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(80, 0, 0))
    }),
    StrokeColor = Color3.fromRGB(255, 60, 60),
    StrokeTransparency = 0.2,
    OnlyMobile = false,
    Enabled = true,
    Draggable = true,
    Shadow = true,
    ShadowTransparency = 0.4,
    ShadowColor = Color3.fromRGB(40, 0, 0),
    }
})


local keybindFile = "keybind_config.txt"

local function getCleanKeyName(keyCode)
    local keyString = tostring(keyCode)
    return keyString:gsub("Enum%.KeyCode%.", "")
end

local function saveKeybind(keyCode)
    writefile(keybindFile, tostring(keyCode))
end

local function loadKeybind()
    if isfile(keybindFile) then
        local savedKey = readfile(keybindFile)
        for _, key in pairs(Enum.KeyCode:GetEnumItems()) do
            if tostring(key) == savedKey then
                return key
            end
        end
    end
    return Enum.KeyCode.F
end

local initialKey = loadKeybind()
local initialKeyName = getCleanKeyName(initialKey)
Window:SetToggleKey(initialKey)

local function RainbowColor(speed)
    return Color3.fromHSV((tick() * speed) % 1, 1, 1)
end

-- ===============================
-- ===============================
-- PREMIUM TAG (RAINBOW)
-- ===============================
local tag = Window:Tag({
    Title = "PREMIUM SCRIPT",
    Icon = "github",
    Color = Color3.fromRGB(255,255,255)
})

-- Rainbow warna (halus, time-based)
task.spawn(function()
    local t = 0
    while task.wait(0.1) do
        t += 0.03
        local r = math.sin(t) * 127 + 128
        local g = math.sin(t + 2) * 127 + 128
        local b = math.sin(t + 4) * 127 + 128
        tag:SetColor(Color3.fromRGB(r, g, b))
    end
end)

-- ===============================
-- FPS & PING OVERLAY (AMAN UI)
-- ===============================
local RunService = game:GetService("RunService")
local Stats = game:GetService("Stats")
local Players = game:GetService("Players")

local player = Players.LocalPlayer
local pg = player:WaitForChild("PlayerGui")

-- hapus overlay lama kalau re-execute
local old = pg:FindFirstChild("PerfOverlay")
if old then old:Destroy() end

local gui = Instance.new("ScreenGui")
gui.Name = "PerfOverlay"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.DisplayOrder = 1000000
gui.Parent = pg

local label = Instance.new("TextLabel")
label.Size = UDim2.new(0, 190, 0, 24)
label.Position = UDim2.new(1, -200, 0, 6) -- kanan atas
label.BackgroundTransparency = 1
label.TextXAlignment = Enum.TextXAlignment.Left
label.TextYAlignment = Enum.TextYAlignment.Center
label.Font = Enum.Font.SourceSansBold
label.TextSize = 14
label.TextColor3 = Color3.fromRGB(255,255,255)
label.TextStrokeTransparency = 0.4
label.Text = "FPS: -- | PING: --"
label.Parent = gui

-- FPS counter (ringan)
local frames, fps = 0, 0
local last = tick()

RunService.RenderStepped:Connect(function()
    frames += 1
    local now = tick()
    if now - last >= 0.5 then
        fps = math.floor(frames / (now - last))
        frames = 0
        last = now
    end
end)

-- Update FPS & Ping
task.spawn(function()
    while task.wait(0.5) do
        local ping = 0
        pcall(function()
            ping = math.floor(
                Stats.Network.ServerStatsItem["Data Ping"]:GetValue()
            )
        end)

        label.Text = string.format("FPS: %d | PING: %d ms", fps, ping)
    end
end)




task.spawn(function()
    while true do
        task.wait()

        -- Jika tag object hilang → break
        if not tag then 
            break 
        end

        -- Coba set color, kalau error → break
        local ok = pcall(function()
            tag:SetColor(RainbowColor(0.6))
        end)

        if not ok then
            break
        end
    end
end)


Window:SetUIScale(0.65)



--======================================================
-- AUTO DEVICE SPOOF
--======================================================
task.spawn(function()
    task.wait(1) 
    local UIS = game:GetService("UserInputService")
    local isMobile = UIS.TouchEnabled and not UIS.KeyboardEnabled

    if isMobile then
        getgenv().DeviceSpoof = {
            TouchEnabled = false,
            KeyboardEnabled = true,
            MouseEnabled = true,
            Device = "PC (Spoofed)"
        }
        DimszyHUB16:Notify({Title = "Device Spoof", Content = "Mode PC diaktifkan otomatis.", Duration = 3})
    else
        getgenv().DeviceSpoof = {
            TouchEnabled = UIS.TouchEnabled,
            KeyboardEnabled = UIS.KeyboardEnabled,
            MouseEnabled = UIS.MouseEnabled,
            Device = "PC"
        }
    end
end)

---------------------------------------------------------------------
-- 🔐 KEY SYSTEM (MERGED FROM key_system.lua) – NO LOADFILE
---------------------------------------------------------------------

local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RobloxUsername = LocalPlayer.Name
-- File config

local FILE_CONFIG = {
    folder = "davidscripts",
    subfolder = "auth",
    filename = "trial.date"
}

-- Function get auth file path
local function getAuthFilePath()
    return FILE_CONFIG.folder .. "/" .. FILE_CONFIG.subfolder .. "/" .. FILE_CONFIG.filename
end

-- Function save token
local function saveToken(token)
    local success, err = pcall(function()
        if not isfolder(FILE_CONFIG.folder) then
            makefolder(FILE_CONFIG.folder)
        end
        
        local authFolder = FILE_CONFIG.folder .. "/" .. FILE_CONFIG.subfolder
        if not isfolder(authFolder) then
            makefolder(authFolder)
        end
        
        local data = {
            token = token,
            username = RobloxUsername,
            saved_at = os.time(),
            version = "1.0"
        }
        
        writefile(getAuthFilePath(), HttpService:JSONEncode(data))
    end)
    
    if not success then
        warn("[AUTH] Gagal menyimpan token: " .. tostring(err))
    end
    
    return success
end

-- Function load token
local function loadToken()
    local success, result = pcall(function()
        if not isfile(getAuthFilePath()) then
            return nil
        end
        
        local content = readfile(getAuthFilePath())
        local data = HttpService:JSONDecode(content)
        
        if data.username == RobloxUsername then
            return data.token
        else
            return nil
        end
    end)
    
    if success then
        return result
    else
        warn("[AUTH] Failed to load token: " .. tostring(result))
        return nil
    end
end

-- Function delete token
local function deleteToken()
    pcall(function()
        if isfile(getAuthFilePath()) then
            delfile(getAuthFilePath())
        end
    end)
end

-- Api Config
local API_CONFIG = {
    base_url = "https://dimszyhub.my.id/",
    validate_endpoint = "validate.php",
}

-- Function safe http request (IMPROVED)
local function safeHttpRequest(url, method, data, headers)
    method = method or "GET"
    
    -- Add default headers for ngrok
    if not headers then
        headers = {}
    end
    headers["ngrok-skip-browser-warning"] = "true"
    
    -- Method 1: RequestAsync (paling reliable)
    local requestData = {
        Url = url,
        Method = method,
        Headers = headers
    }
    
    if data and method == "POST" then
        requestData.Body = data
    end
    
    local ok, res = pcall(function()
        return HttpService:RequestAsync(requestData)
    end)
    
    if ok and res then
        if res.Success and res.StatusCode == 200 then
            return true, res.Body
        elseif res.Success then
            return false, "HTTP Error: " .. (res.StatusCode or "Unknown") .. " - " .. tostring(res.Body or "")
        else
            return false, "Request failed: " .. tostring(res.StatusMessage or "Unknown")
        end
    end

    -- Method 2: GetAsync (fallback untuk GET requests)
    if method == "GET" then
        local ok2, res2 = pcall(function()
            return HttpService:GetAsync(url, true, headers)
        end)
        if ok2 and res2 then 
            return true, res2 
        end

        -- Method 3: game:HttpGet (last resort)
        local ok3, res3 = pcall(function()
            return game:HttpGet(url)
        end)
        if ok3 and res3 then 
            return true, res3 
        end
        
        return false, "All HTTP methods failed: " .. tostring(res)
    end

    return false, "HTTP request failed: " .. tostring(res)
end

-- Function validate token
local function ValidateToken(token)
    if not token or token == "" then
        return false, "Token tidak boleh kosong!"
    end

    local encodedToken = HttpService:UrlEncode(tostring(token))
    local encodedUsername = HttpService:UrlEncode(tostring(RobloxUsername))
    local url = API_CONFIG.base_url .. "/" .. API_CONFIG.validate_endpoint .. "?token=" .. encodedToken .. "&roblox_username=" .. encodedUsername
    
    local headers = {
        ["Content-Type"] = "application/json",
        ["User-Agent"] = "Roblox/WinInet",
        ["ngrok-skip-browser-warning"] = "true"
    }

    local ok, res = safeHttpRequest(url, "GET", nil, headers)
    if not ok then
        return false, "Connection error: " .. tostring(res)
    end

    local okDecode, data = pcall(function()
        return HttpService:JSONDecode(res)
    end)
    
    if not okDecode then
        return false, "Invalid server response format: " .. tostring(res):sub(1, 100)
    end
    
    if type(data) ~= "table" then
        return false, "Invalid server response structure"
    end

    if tostring(data.status or ""):lower() == "success" then
        return true, data
    else
        local errorMsg = tostring(data.message or "Authentication failed")
        return false, errorMsg
    end
end


---------------------------------------------------------------------
-- 🔐 KEY LOGIN TAB (FIXED)
---------------------------------------------------------------------

local Tabs = {
    WalkTab = nil,
    SettingsTab = nil, 
    RunAnimationTab = nil,
    MainTab = nil, 
}



-- Konfigurasi Mounts

local MOUNT_CONFIG_URL = "mt.lua"
local ok, MountData = pcall(function()
    return loadstring(game:HttpGet(getSecureURL(MOUNT_CONFIG_URL)))()
end) 

local FloatingMounts = {}
local CheckpointMounts = {}

if ok and MountData and MountData.FloatingMounts and MountData.CheckpointMounts then
    FloatingMounts = MountData.FloatingMounts
    CheckpointMounts = MountData.CheckpointMounts
else
    DimszyHUB16:Notify({ Title = "Mount Config", Content = "Gagal memuat konfigurasi mount.", Duration = 3 })
end




---------------------------------------------------------------------
-- STATE
---------------------------------------------------------------------
local isPlaying = false
local isPaused = false
local isFlipped = false
local playbackSpeed = 1.0
local playbackConnection = nil
local heightOffset = 0
local FLIP_SMOOTHNESS = 0.15
local currentFlipRotation = CFrame.new()
local isLoopingEnabled = false
local isLoopingActive = false
local currentMountName = nil
local currentMountType = nil 
local antiAfkConnection = nil
local activeUIElements = {} 
local V1_JSON_EXISTS = false
local V2_JSON_EXISTS = false
local V3_JSON_EXISTS = false
local baseURL = ""
local currentFloatingPath = nil

---------------------------------------------------------------------
-- UTIL
---------------------------------------------------------------------
local function vecToTable(v3)
    return {x = v3.X, y = v3.Y, z = v3.Z}
end
local function tableToVec(t)
    if not t then return Vector3.new(0,0,0) end
    return Vector3.new(t.x or 0, t.y or 0, t.z or 0)
end
local function lerp(a,b,t) return a + (b-a)*t end
local function lerpVector(a,b,t) return Vector3.new(lerp(a.X,b.X,t), lerp(a.Y,b.Y,t), lerp(a.Z,b.Z,t)) end 
local function lerpAngle(a,b,t)
    local diff = (b - a)
    while diff > math.pi do diff = diff - 2*math.pi end
    while diff < -math.pi do diff = diff + 2*math.pi end
    return a + diff * t
end

local function findSurroundingFrames(data, t)
    if #data == 0 then return 1,1,0 end
    if t <= data[1].time then return 1,1,0 end
    if t >= data[#data].time then return #data,#data,0 end
    local left, right = 1, #data
    while left < right - 1 do
        local mid = math.floor((left + right) / 2)
        if data[mid].time <= t then left = mid else right = mid end
    end
    local span = data[right].time - data[left].time
    local alpha = span > 0 and math.clamp((t - data[left].time) / span, 0, 1) or 0
    return left, right, alpha
end


-- Fungsi helper untuk mendapatkan direktori (akan mengembalikan "" jika hanya nama file)
local function getDirectoryPath(filePath)
    -- Mencari slash terakhir (asumsi menggunakan forward slash '/')
    local lastSlash = string.find(filePath, "/[^/]*$")
    if lastSlash then
        -- Mengembalikan string path hingga slash terakhir, yang menjadi directory path
        return string.sub(filePath, 1, lastSlash)
    end
    -- Jika tidak ada slash, file berada di root relatif (kembalikan string kosong)
    return "" 
end

local MOUNT_DATA_SUBFOLDER = "mount_data"


local function getInternalMountPath(mountBaseName, fileName)
    local safeMountName = mountBaseName:gsub("[^a-zA-Z0-9_]", "_")
    local mountFolder = FILE_CONFIG.folder .. "/" .. MOUNT_DATA_SUBFOLDER .. "/" .. safeMountName
    return mountFolder .. "/" .. fileName
end

local function ensureMountFolders(mountBaseName)
    local safeMountName = mountBaseName:gsub("[^a-zA-Z0-9_]", "_")
    if not isfolder(FILE_CONFIG.folder) then
        makefolder(FILE_CONFIG.folder)
    end
    
    local dataSubfolder = FILE_CONFIG.folder .. "/" .. MOUNT_DATA_SUBFOLDER
    if not isfolder(dataSubfolder) then
        makefolder(dataSubfolder)
    end

    local mountFolder = dataSubfolder .. "/" .. safeMountName
    if not isfolder(mountFolder) then
        makefolder(mountFolder)
    end
end




local function LoadJsonAsync_Download(actualPath, callback)
    local fileNameOnly
    local lastSlash = actualPath:find("[^/]*$")
    if lastSlash then
        fileNameOnly = actualPath:sub(lastSlash)
    else
        fileNameOnly = actualPath
    end

    local mountBaseName = currentMountName
    local internalFilePath = getInternalMountPath(mountBaseName, fileNameOnly) 

    task.spawn(function()
        DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Mengunduh file JSON dari server...", Duration = 1.5 })
   
        local url = getSecureURL(actualPath)
        local ok, res = pcall(function() return game:HttpGet(url) end)
        
        if not ok or not res or type(res) ~= "string" or res:len() == 0 then 
            DimszyHUB16:Notify({ Title = "Error", Content = "Gagal mengunduh file JSON: Koneksi/Server.", Duration = 3 })
            callback(nil) 
            return 
        end
        
        local ok2, data = pcall(function() return HttpService:JSONDecode(res) end)
        
        if ok2 and type(data) == "table" then
            JsonCache[actualPath] = data
            callback(data)
            
            if currentMountType == "CHECKPOINT" then
                
                ensureMountFolders(mountBaseName)
                
                local successWrite, errWrite = pcall(writefile, internalFilePath, res)
                
                if successWrite then
                    DimszyHUB16:Notify({ Title = "Auto Walk", Content = "JSON berhasil diunduh & disimpan lokal.", Duration = 1.5 })
                else
                    warn("[Auto Walk] GAGAL menyimpan JSON lokal: " .. tostring(errWrite) .. " | Path yang gagal: " .. internalFilePath)
                    DimszyHUB16:Notify({ Title = "Error", Content = "Gagal menyimpan JSON lokal (Cek Console).", Duration = 3 })
                end
            end
            
        else
            DimszyHUB16:Notify({ Title = "Error", Content = "Format JSON tidak valid setelah diunduh.", Duration = 3 })
            callback(nil)
        end
    end)
end

-- JSON CACHE
local function LoadJsonAsync(file, callback)
    local actualPath
    if currentFloatingPath then
        actualPath = currentFloatingPath -- 
    else
        actualPath = baseURL .. file
    end
    
    local fileNameOnly

    local lastSlash = actualPath:find("[^/]*$")
    if lastSlash then
        fileNameOnly = actualPath:sub(lastSlash)
    else
        fileNameOnly = actualPath 
    end
    
    if JsonCache[actualPath] then
        callback(JsonCache[actualPath])
        return
    end

    if actualPath == "" then
        DimszyHUB16:Notify({ Title = "Error", Content = "Path file tidak valid. Pilih Mount terlebih dahulu!", Duration = 3 })
        callback(nil)
        return
    end
    local mountBaseName = currentMountName
    local internalFilePath = getInternalMountPath(mountBaseName, fileNameOnly) 

    if currentMountType == "CHECKPOINT" and isfile(internalFilePath) then
        task.spawn(function()
            DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Memuat JSON dari penyimpanan internal...", Duration = 1 })
            
            local okRead, content = pcall(readfile, internalFilePath)
            if okRead and content and content:len() > 0 then
                local okDecode, data = pcall(function() return HttpService:JSONDecode(content) end)
                if okDecode and type(data) == "table" then
                    JsonCache[actualPath] = data -- Cache menggunakan actualPath
                    callback(data)
                    return
                end
            end
            DimszyHUB16:Notify({ Title = "Auto Walk", Content = "File lokal rusak/gagal dimuat, mencoba download ulang...", Duration = 2 })
            
            -- Panggil LoadJsonAsync_Download dengan path yang benar
            LoadJsonAsync_Download(actualPath, callback) 
        end)
        return
    end
    
    -- Panggil LoadJsonAsync_Download dengan path yang benar
    LoadJsonAsync_Download(actualPath, callback)
end

-- Fungsi untuk deteksi ketersediaan file JSON
local function CheckFileOnly(fullPath, callback)
    task.spawn(function()
        local url = getSecureURL(fullPath)
        local ok, res = pcall(function() 
            return game:HttpGet(url) 
        end)
        local fileExists = false
        if ok and res and type(res) == "string" and res:len() > 0 then 
            fileExists = true
        end
        callback(fileExists)
    end)
end

-- Fungsi untuk deteksi ketersediaan file JSON
local function CheckFileOnly(fullPath, callback)
    task.spawn(function()
        local url = getSecureURL(fullPath)
        local ok, res = pcall(function() 
            return game:HttpGet(url) 
        end)
        local fileExists = false
        if ok and res and type(res) == "string" and res:len() > 0 then 
            fileExists = true
        end
        callback(fileExists)
    end)
end


---------------------------------------------------------------------
-- Footstep sound & natural movement
---------------------------------------------------------------------
local footstepSoundTemplate = Instance.new("Sound")
footstepSoundTemplate.Name = "AutoWalkFootstepTemplate"
footstepSoundTemplate.Volume = 1
footstepSoundTemplate.Looped = false

local function playFootstepSoundForMaterial(hrp, material)
    local sound = footstepSoundTemplate:Clone()
    sound.RollOffMaxDistance = 100
    sound.RollOffMinDistance = 10
    local soundId = "rbxasset://sounds/action_footsteps_plastic.mp3"
    if material == Enum.Material.Grass then soundId = "rbxassetid://9118823107"
    elseif material == Enum.Material.Metal then soundId = "rbxassetid://260433111"
    elseif material == Enum.Material.Sand then soundId = "rbxassetid://9120089994"
    elseif material == Enum.Material.Wood then soundId = "rbxassetid://9118828605" end
    sound.SoundId = soundId
    sound.Parent = hrp
    sound:Play()
    Debris:AddItem(sound, 1.5)
end

local lastFootstepTime = 0
local footstepInterval = 0.35
local leftFoot = true

local function playFootstepIfNeeded(moveVelocity, hrp)
    if not humanoid or not character or not hrp then return end
    local horizontal = Vector3.new(moveVelocity.X, 0, moveVelocity.Z)
    local speed = horizontal.Magnitude
    local onGround = false
    pcall(function()
        local state = humanoid:GetState()
        onGround = (state == Enum.HumanoidStateType.Running or
                    state == Enum.HumanoidStateType.RunningNoPhysics or
                    state == Enum.HumanoidStateType.Landed)
    end)
    if speed > 0.5 and onGround then
        local now = tick()
        local speedMultiplier = math.clamp(speed / 16, 0.3, 2)
        local adjustedInterval = footstepInterval / (speedMultiplier * playbackSpeed)
        if now - lastFootstepTime >= adjustedInterval then
            local rayOrigin = hrp.Position
            local rayDirection = Vector3.new(0, -5, 0)
            local rayParams = RaycastParams.new()
            rayParams.FilterDescendantsInstances = {character}
            rayParams.FilterType = Enum.RaycastFilterType.Exclude
            local res = workspace:Raycast(rayOrigin, rayDirection, rayParams)
            local mat = res and res.Material or Enum.Material.Plastic
            playFootstepSoundForMaterial(hrp, mat)
            lastFootstepTime = now
            leftFoot = not leftFoot
        end
    end
end

local function simulateNaturalMovement(moveDirection, velocity, hrp)
    if not humanoid or not character then return end
    local horizontalVelocity = Vector3.new(velocity.X or 0, 0, velocity.Z or 0)
    local speed = horizontalVelocity.Magnitude
    local onGround = false
    pcall(function()
        local state = humanoid:GetState()
        onGround = (state == Enum.HumanoidStateType.Running or
                    state == Enum.HumanoidStateType.RunningNoPhysics or
                    state == Enum.HumanoidStateType.Landed)
    end)
    if speed > 0.5 and onGround then
        pcall(function() humanoid:Move(moveDirection, false) end)
pcall(function() 
    playFootstepIfNeeded(velocity, hrp) 
end)
    else
        pcall(function() humanoid:Move(Vector3.new(0,0,0), false) end)
    end
end

local function walkToPoint(position, callback)
    local player = game.Players.LocalPlayer
    local character = player.Character
    if not character then return end
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    local hrp = character:FindFirstChild("HumanoidRootPart")
    if not humanoid or not hrp then return end

    task.spawn(function()
        local startNotified = false
        while isPlaying and (hrp.Position - position).Magnitude > 5 do
            if not startNotified then
                -- DimszyHUB16:Notify({ Title = "🚶 Auto Walk: Menuju Titik Start", Content = "Menuju titik start...", Duration = 2 })
                 startNotified = true
            end
            humanoid:MoveTo(position)
            task.wait(0.1)
        end
        if isPlaying and callback then 
            if startNotified then
                --DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Sampai di titik start, memulai playback...", Duration = 1 })
            end
            callback() 
        end
    end)
end

-- STARTPLAYBACK 
local function stopPlayback(forceStopLoop)
    isPlaying = false
    isPaused = false
    if forceStopLoop then isLoopingActive = false end
    if playbackConnection then playbackConnection:Disconnect() playbackConnection = nil end
    if humanoid and humanoid.Parent == character then
        pcall(function() humanoid:Move(Vector3.new(0,0,0), false) end)
    end
end

local function StartPlayback(frames, onComplete, startIndexOrTime)
    if not frames or #frames == 0 then
        if onComplete then pcall(onComplete) end
        return
    end
    stopPlayback(false) 

    pcall(function()
        if humanoid and frames[1].hipHeight then
            heightOffset = humanoid.HipHeight - (frames[1].hipHeight or 2)
        else
            heightOffset = 0
        end
    end)

    isPlaying = true
    isPaused = false
    local lastPlaybackTime = tick()
    local accumulatedTime = 0
    local lastJumping = false

    if startIndexOrTime then
        if type(startIndexOrTime) == "number" then
            if math.floor(startIndexOrTime) == startIndexOrTime and startIndexOrTime >=1 and startIndexOrTime <= #frames then
                accumulatedTime = frames[startIndexOrTime].time or 0
            else
                accumulatedTime = math.max(0, startIndexOrTime)
            end
        end
    end

    playbackConnection = RunService.Heartbeat:Connect(function(deltaTime)
        if not isPlaying then return end
        if isPaused then lastPlaybackTime = tick() return end

        local now = tick()
        local dt = math.min(now - lastPlaybackTime, 0.1)
        lastPlaybackTime = now
        accumulatedTime = accumulatedTime + dt * playbackSpeed

        if accumulatedTime > frames[#frames].time then
            local shouldStop = not (isLoopingEnabled and onComplete) -- Hentikan hanya jika tidak sedang looping
            
            if shouldStop then
                isPlaying = false 
            end
            
            if playbackConnection then playbackConnection:Disconnect() playbackConnection = nil end
            
            if onComplete then pcall(onComplete) end
            
            if shouldStop then
                return
            end
        end
        if _G.__ForceStopPlayback then return end

        local i0,i1,alpha = findSurroundingFrames(frames, accumulatedTime)
        local f0, f1 = frames[i0], frames[i1]
        if not f0 or not f1 then return end

        local p0 = tableToVec(f0.position)
        local p1 = tableToVec(f1.position)

        local vel0, vel1
        if f0.velocity then vel0 = tableToVec(f0.velocity) else
            local dtf = math.max((f1.time - f0.time), 0.001)
            vel0 = (p1 - p0) / dtf
        end
        if f1.velocity then vel1 = tableToVec(f1.velocity) else
            local dtf = math.max((f1.time - f0.time), 0.001)
            vel1 = (p1 - p0) / dtf
        end

        local move0 = f0.moveDirection and tableToVec(f0.moveDirection) or Vector3.new(vel0.X, vel0.Y, vel0.Z).Unit
        local move1 = f1.moveDirection and tableToVec(f1.moveDirection) or Vector3.new(vel1.X, vel1.Y, vel1.Z).Unit
        
        local yaw0 = f0.rotation or 0
        local yaw1 = f1.rotation or yaw0
        if (yaw0 == 0 and yaw1 == 0) then
            local dir = (p1 - p0)
            if dir.Magnitude > 0.01 then
                yaw0 = math.atan2(-dir.Z, dir.X)
                yaw1 = yaw0
            end
        end

        local jumping0 = f0.jumping or false
        local jumping1 = f1.jumping or false
        if f0.jumping == nil and f1.jumping == nil then
            local vy0 = vel0.Y or 0
            local vy1 = vel1.Y or 0
            jumping0 = vy0 > 1
            jumping1 = vy1 > 1
        end

        local interpPos = lerpVector(p0, p1, alpha)
        local interpVel = lerpVector(vel0, vel1, alpha)
        local interpMove = lerpVector(move0, move1, alpha)
        local interpYaw = lerpAngle(yaw0, yaw1, alpha)
        local jumpingNow = jumping0 or jumping1

        local hrp = (character and character:FindFirstChild("HumanoidRootPart"))
        if not hrp then return end

        local correctedY = interpPos.Y + (heightOffset or 0)
        local targetCFrame = CFrame.new(interpPos.X, correctedY, interpPos.Z) * CFrame.Angles(0, interpYaw, 0)

        local function smoothLerpCF(current, target, deltaTime)
            local t = 1 - math.exp(-14 * deltaTime)
            return current:Lerp(target, t)
        end

        local targetFlip = isFlipped and CFrame.Angles(0, math.pi, 0) or CFrame.new()
        currentFlipRotation = currentFlipRotation:Lerp(targetFlip, FLIP_SMOOTHNESS)
        hrp.CFrame = smoothLerpCF(hrp.CFrame, targetCFrame * currentFlipRotation, deltaTime)

        pcall(function() hrp.AssemblyLinearVelocity = interpVel end)
        pcall(function()
            if humanoid and humanoid.Parent == character then
                humanoid:Move(interpMove, false)
            end
        end)
        simulateNaturalMovement(interpMove, interpVel, hrp)

        if jumpingNow and not lastJumping then
            pcall(function()
                if humanoid then humanoid:ChangeState(Enum.HumanoidStateType.Jumping) end
            end) 
        end
        lastJumping = jumpingNow
    end)
end


local function playSingleCheckpointFile(fileName, idx, files)
    stopPlayback(true)
    isPlaying = true 

    LoadJsonAsync(fileName, function(data)
        if not data or #data == 0 then 
            stopPlayback(true) 
            SimpleFloatingControls.Hide()
            DimszyHUB16:Notify({ Title = "Auto Walk", Content = "JSON gagal dimuat untuk checkpoint ini.", Duration = 3 })
            return 
        end
        
        local hrp = (character and character:FindFirstChild("HumanoidRootPart"))
        if not hrp then return end
        
        local nearestIndex = 1
        local nearestDist = math.huge
        local hrpPos = hrp.Position
        local nearestPoint = tableToVec(data[1].position) 

        -- Cari frame terdekat
        for i, frame in ipairs(data) do
            if frame.position then
                local pos = tableToVec(frame.position)
                local d = (hrpPos - pos).Magnitude
                if d < nearestDist then
                    nearestDist = d
                    nearestIndex = i
                    nearestPoint = pos 
                end
            end
        end
        
        if nearestDist > 100 then
    local contentMessage = string.format("Di luar area (%.0f studs).", nearestDist)
    
    DimszyHUB16:Notify({
        Title = "Auto Walk",
        Content = contentMessage, 
        Duration = 3
    })
    
    stopPlayback(true)
    SimpleFloatingControls.Hide() 
    return
end


        local function startPath()
            StartPlayback(data, function()
                DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Checkpoint selesai!", Duration = 2 })
                
                -- PERBAIKAN DI SINI: Hapus 'and isPlaying == false'
                if isLoopingEnabled then 
                    local nextIdx = idx + 1
                    local isWrapping = false
                    if nextIdx > #files then 
                        nextIdx = 1
                        isWrapping = true
                    end
                    local nextInfo = files[nextIdx]
                    
                    if nextInfo then
                        -- Set isPlaying ke true sebelum memulai loop berikutnya
                        isPlaying = true 
                       -- DimszyHUB16:Notify({ Title = "Auto Loop", Content = "Lanjut ke " .. nextInfo.name .. (isWrapping and " (Cycle)" or "") .. "...", Duration = 1 })
                      --  task.delay(0.5, function()
                            playSingleCheckpointFile(nextInfo.file, nextIdx, files)
                     --   end)
                    else
                         SimpleFloatingControls.Hide()
                    end
                else
                    SimpleFloatingControls.Hide() 
                end
            end, nearestIndex)
        end
        
        if nearestDist > 2 then
            local hLocal = character:FindFirstChildOfClass("Humanoid")
            if hLocal then
                walkToPoint(nearestPoint, function() 
                    startPath()
                end)
            else
                -- DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Memulai Auto Walk dari frame terdekat.", Duration = 1 })
                startPath()
            end
        else
           -- DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Memulai Auto Walk dari frame terdekat.", Duration = 1 })
            startPath()
        end
    end)
end
---------------------------------------------------------------------
-- Floating UI (Checkpoint/Simple) - REVISI DARI SEBELUMNYA
---------------------------------------------------------------------
local function CreateFloatingAutoWalkUI1()
    local gui = Instance.new("ScreenGui")
    gui.Name = "FloatingAutoWalkUI_Simple" 
    gui.ResetOnSpawn = false
    gui.Parent = CoreGui

    -- Frame Utama (Container)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 105, 0, 50) 
    frame.Position = UDim2.new(0.5, -80, 0.60, 0)
    frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30) 
    frame.BackgroundTransparency = 0.25
    frame.Active = true
    frame.Draggable = true
    frame.Parent = gui

    Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 10) 
    local stroke = Instance.new("UIStroke", frame)
    stroke.Color = Color3.fromRGB(50, 50, 50)
    stroke.Thickness = 1
    
    local layout = Instance.new("UIListLayout")
    layout.FillDirection = Enum.FillDirection.Horizontal
    layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
    layout.VerticalAlignment = Enum.VerticalAlignment.Center
    layout.Padding = UDim.new(0, 5) 
    layout.Parent = frame
    
    -- Warna Modern
    local DEFAULT_COLOR = Color3.fromRGB(50, 50, 50)         
    local ACTIVE_COLOR = Color3.fromRGB(255, 60, 60)      
    local PAUSE_COLOR = Color3.fromRGB(255, 170, 0)          
    local STOP_COLOR = Color3.fromRGB(255, 70, 70)           

    -- TEMPLATE BUTTON
    local function makeBtn(text)
        local btn = Instance.new("TextButton")
        btn.Size = UDim2.new(0, 48, 0, 40) 
        btn.BackgroundColor3 = DEFAULT_COLOR
        btn.Text = text
        btn.Font = Enum.Font.GothamBold
        btn.TextSize = 16
        btn.TextColor3 = Color3.fromRGB(220, 220, 220) 
        btn.TextWrapped = true
        Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 8) 
        btn.Parent = frame
        return btn
    end

    local controlBtn = makeBtn("STOP") 
    local flipBtn = makeBtn("FLIP")
    
    local function updateControlBtnVisual(isCurrentlyPlaying, isCurrentlyPaused)
        if not controlBtn.Parent then return end
        
        if isCurrentlyPlaying then
            if isCurrentlyPaused then
                controlBtn.Text = "RESUME"
                controlBtn.BackgroundColor3 = PAUSE_COLOR
            else
                controlBtn.Text = "STOP"
                controlBtn.BackgroundColor3 = STOP_COLOR
            end
        else
            controlBtn.Text = "STOP" 
            controlBtn.BackgroundColor3 = DEFAULT_COLOR
        end
        
        flipBtn.BackgroundColor3 = isFlipped and ACTIVE_COLOR or DEFAULT_COLOR
        flipBtn.TextColor3 = isFlipped and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(180, 180, 180)
    end

    -- STOP/RESUME logic
    controlBtn.MouseButton1Click:Connect(function()
        if isPlaying and not isPaused then
            isPaused = true
            DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Paused.", Duration = 1 })

        elseif isPlaying and isPaused then
            isPaused = false
            DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Resume.", Duration = 1 })

        else
            stopPlayback(true) 
            DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Auto walk dihentikan.", Duration = 2 })
            SimpleFloatingControls.Hide() 
            
            if currentMountType == "CHECKPOINT" then
                for _, otherTg in ipairs(activeUIElements) do
                    if otherTg.Type == "Toggle" and string.sub(otherTg.Title, 1, 1) ~= "S" and otherTg.CurrentValue then
                        otherTg:SetValue(false)
                    end
                end
            end
        end
        updateControlBtnVisual(isPlaying, isPaused)
    end)
    
    
    -- Monitor status global
    task.spawn(function()
        local lastPlaying = false
        local lastPaused = false
        local lastFlipped = false
        while task.wait(0.1) do
            if isPlaying ~= lastPlaying or isPaused ~= lastPaused or isFlipped ~= lastFlipped then
                updateControlBtnVisual(isPlaying, isPaused)
                lastPlaying = isPlaying
                lastPaused = isPaused
                lastFlipped = isFlipped
            end
        end
    end)


    -- FLIP logic
    flipBtn.MouseButton1Click:Connect(function()
        if isPlaying then
            isFlipped = not isFlipped
            updateControlBtnVisual(isPlaying, isPaused) 
            DimszyHUB16:Notify({
                Title = "Auto Walk",
                Content = isFlipped and "Flip aktif." or "Flip mati.",
                Duration = 1
            })
        else
            DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Auto walk belum berjalan.", Duration = 1 })
        end
    end)

    frame.Visible = false

    return {
        Show = function() 
            frame.Visible = true 
            updateControlBtnVisual(isPlaying, isPaused) 
        end,
        Hide = function() frame.Visible = false end,
        Reset = function() frame.Visible = false; isPaused = false; isFlipped = false end
    }
end

local SimpleFloatingControls = CreateFloatingAutoWalkUI1()
---------------------------------------------------------------------
-- Floating UI (Floating V1/V2) - REVISI DARI SEBELUMNYA
---------------------------------------------------------------------
local function CreateFloatingAutoWalkUI()
    local gui = Instance.new("ScreenGui")
    gui.Name = "FloatingAutoWalkUI_Complex"
    gui.ResetOnSpawn = false
    gui.Parent = CoreGui

    local frame = Instance.new("Frame")
    -- Ukuran dan Posisi tetap sama
    frame.Size = UDim2.new(0, 160, 0, 50)
    frame.Position = UDim2.new(0.5, -80, 0.60, 0)
    
    -- Latar Belakang Frame diubah menjadi Hitam (mendekati 0, 0, 0) dengan sedikit transparansi
    frame.BackgroundColor3 = Color3.fromRGB(15, 15, 15) -- Lebih gelap
    frame.BackgroundTransparency = 0.1 -- Sedikit lebih padat
    
    frame.Active = true
    frame.Draggable = true
    frame.Visible = false
    frame.Parent = gui
    Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 10)
    
    local stroke = Instance.new("UIStroke", frame)
    -- Stroke diubah menjadi Merah
    stroke.Color = Color3.fromRGB(200, 0, 0) -- Merah cerah
    stroke.Thickness = 2 -- Sedikit lebih tebal untuk penekanan Merah

    local layout = Instance.new("UIListLayout")
    layout.FillDirection = Enum.FillDirection.Horizontal
    layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
    layout.VerticalAlignment = Enum.VerticalAlignment.Center
    layout.Padding = UDim.new(0, 4) 
    layout.Parent = frame

    -- Warna Modern
    local DEFAULT_COLOR = Color3.fromRGB(50, 50, 50)         
    local ACTIVE_COLOR = Color3.fromRGB(0, 200, 0)
    local FLIP_ACTIVE_COLOR = Color3.fromRGB(255, 170, 0)    
    
    local function makeBtn(text)
    local b = Instance.new("TextButton")
    
    b.Size = UDim2.new(0, 48, 0, 40)
    
    -- Latar Belakang Tombol: Hitam Gelap
    b.BackgroundColor3 = Color3.fromRGB(20, 20, 20) 
    
    b.Text = text
    b.Font = Enum.Font.GothamBold
    b.TextSize = 16
    
    -- Teks Tombol: Putih/Abu-abu Cerah agar mudah dibaca di latar belakang gelap
    b.TextColor3 = Color3.fromRGB(220, 220, 220) 
    
    Instance.new("UICorner", b).CornerRadius = UDim.new(0, 8)
    
    -- Tambahkan Line Merah (UIStroke)
    local stroke = Instance.new("UIStroke", b)
    stroke.Color = Color3.fromRGB(255, 0, 0) -- Merah Murni
    stroke.Thickness = 2 -- Ketebalan Garis
    stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border -- Pastikan stroke hanya pada border

    b.Parent = frame
    return b
end

    local V1 = makeBtn("V1")
    local V2 = makeBtn("V2")
    local V3 = makeBtn("V3") -- Tombol V3 baru
    local FLIP = makeBtn("FLIP")
    
    local currentActivePath = nil 
    local isFlipActive = isFlipped 

    local function setActivePathButtonColor(pathName)
        V1.BackgroundColor3 = (pathName == "V1") and ACTIVE_COLOR or DEFAULT_COLOR
        V2.BackgroundColor3 = (pathName == "V2") and ACTIVE_COLOR or DEFAULT_COLOR
        V3.BackgroundColor3 = (pathName == "V3") and ACTIVE_COLOR or DEFAULT_COLOR
        
        V1.TextColor3 = (pathName == "V1") and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(180, 180, 180)
        V2.TextColor3 = (pathName == "V2") and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(180, 180, 180)
        V3.TextColor3 = (pathName == "V3") and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(180, 180, 180)
    end
    
    
    local function startPlay(file, isLoopRunCycle) 
        stopPlayback(false)
        isPlaying = true 

        LoadJsonAsync(file, function(data)
            if not data or #data == 0 then
                stopPlayback(true)
                currentActivePath = nil
                setActivePathButtonColor(nil)
                DimszyHUB16:Notify({ Title = "Auto Walk", Content = "JSON gagal dimuat! (" .. baseURL .. file .. ")", Duration = 2 })
                
                if not V1_JSON_EXISTS and not V2_JSON_EXISTS and not V3_JSON_EXISTS then frame.Visible = false end

                return
            end
            
            local char = game:GetService("Players").LocalPlayer.Character
            if not char or not char:FindFirstChild("HumanoidRootPart") then return end
            local hrp = char.HumanoidRootPart
            local nearestIdx = 1
            local nearestDist = math.huge
            local nearestPoint = Vector3.new()

            local isStartingNewCycle = isLoopingEnabled and isLoopRunCycle
            
            if isStartingNewCycle then
                nearestIdx = 1
                if data[1] and data[1].position then
                    nearestPoint = tableToVec(data[1].position)
                    nearestDist = (hrp.Position - nearestPoint).Magnitude 
                end
            else
                for i, point in ipairs(data) do
                    if point.position then
                        local pos = tableToVec(point.position)
                        local dist = (hrp.Position - pos).Magnitude
                        if dist < nearestDist then
                            nearestDist = dist
                            nearestIdx = i
                            nearestPoint = pos
                        end
                    end
                end
            end

            local MAX_DIST = 60
            local NEAR_DIST = 3

            if not isStartingNewCycle and nearestDist > MAX_DIST then
                stopPlayback(true)
                currentActivePath = nil
                setActivePathButtonColor(nil)

                DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Terlalu jauh (" .. math.floor(nearestDist) .. " studs)", Duration = 3 })
                return
            end

            setActivePathButtonColor(currentActivePath)

-- KODE YANG HARUS DITEMPELKAN SEBELUM beginPath dipanggil:
            if nearestIndex == #data and not isLoopingEnabled then 
    
    -- Reset index ke 1
           nearestIndex = 1 
    
    -- Reset titik terdekat ke posisi frame pertama
           nearestPoint = tableToVec(data[1].position) 
        end
            local function beginPath()
                _G.__ForceStopPlayback = true
                task.wait(0.1)
                _G.__ForceStopPlayback = false
                StartPlayback(data, function()
                    if isLoopingEnabled then
                        DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Looping...", Duration = 1.5 })
                        
                        task.delay(2.5, function() 
                            if isLoopingEnabled then 
                                startPlay(file, true) 
                            else
                                currentActivePath = nil 
                                setActivePathButtonColor(nil) 
                                DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Loop Dibatalkan.", Duration = 2 })
                            end
                        end) 
                        return
                    end
                    
                    stopPlayback(true) 
                    currentActivePath = nil 
                    setActivePathButtonColor(nil) 
                   -- frame.Visible = false 
                    DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Selesai.", Duration = 2 })
                end, nearestIdx)
            end

            if nearestDist <= NEAR_DIST or isStartingNewCycle then
                -- DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Memulai Auto Walk dari frame terdekat.", Duration = 1 })
                beginPath()
            else
                local hLocal = char:FindFirstChildOfClass("Humanoid")
                if hLocal then
                    walkToPoint(nearestPoint, function()
                        beginPath()
                    end)
                else
                    beginPath()
                end
            end
        end)
    end


    local function handlePathClick(pathName, pathValue)
    if currentMountType ~= "FLOATING" then return end
    
    local isPathAvailable = (pathName == "V1" and V1_JSON_EXISTS) 
    or (pathName == "V2" and V2_JSON_EXISTS)
    or (pathName == "V3" and V3_JSON_EXISTS)

    if not isPathAvailable then
         DimszyHUB16:Notify({ Title = "Auto Walk", Content = pathName .. " JSON tidak tersedia!", Duration = 2 })
         return
    end

    if isPlaying then
        if currentActivePath == pathName then
            stopPlayback(true)
            currentActivePath = nil
            setActivePathButtonColor(nil) 
            DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Dihentikan oleh tombol " .. pathName .. ".", Duration = 2 })
            
            local mountCfg = FloatingMounts[currentMountName]
            
            -- Bagian ini mungkin juga perlu dibersihkan untuk mount baru:
            -- Jika mountConfig.vX adalah path file tunggal (tidak diakhiri '/'), setel baseURL menjadi ""
            baseURL = (V1_JSON_EXISTS and mountCfg.v1) 
                or (V2_JSON_EXISTS and mountCfg.v2) 
                or (V3_JSON_EXISTS and mountCfg.v3)
                or ""
            
            -- Jika baseURL di atas adalah nama file ("mount_yagesya.json"), setel ke ""
            if baseURL and string.sub(baseURL, -5) == ".json" then 
                baseURL = "" 
            end

        else
            local runningPath = currentActivePath or (isPlaying and "jalur saat ini")
            DimszyHUB16:Notify({ 
                Title = "⚠️ Gagal Pindah Jalur", 
                Content = "Harap hentikan " .. runningPath .. " terlebih dahulu sebelum memulai " .. pathName .. ".", 
                Duration = 3 
            })
        end
    
    else
        
        currentActivePath = pathName
        setActivePathButtonColor(pathName)
        
        local fileToStart = pathValue
        
        -- 1. Tentukan apakah ini adalah path folder lama yang butuh main.json
        if pathValue and pathValue ~= "" and string.sub(pathValue, -1) == '/' and string.sub(pathValue, -5) ~= ".json" then
            baseURL = pathValue 
            fileToStart = "main.json" 
        elseif pathValue and string.sub(pathValue, -5) == ".json" then
            -- Kasus: Path file tunggal baru (misal: "mount_yagesya.json").
            baseURL = "" -- Pastikan baseURL dikosongkan untuk path tunggal!
            fileToStart = pathValue
        else
            -- Fallback untuk path folder lama lainnya (asumsikan butuh main.json)
            baseURL = pathValue
            fileToStart = "main.json"
        end

        DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Memulai jalur " .. pathName .. "...", Duration = 1.5 })
        
        -- 2. Panggil startPlay
        startPlay(fileToStart, false) 
    end
end

    V1.MouseButton1Click:Connect(function() 
        local mountCfg = FloatingMounts[currentMountName]
        handlePathClick("V1", mountCfg.v1) 
    end)
    
    V2.MouseButton1Click:Connect(function() 
        local mountCfg = FloatingMounts[currentMountName]
        handlePathClick("V2", mountCfg.v2) 
    end) 

    V3.MouseButton1Click:Connect(function() 
        local mountCfg = FloatingMounts[currentMountName]
        handlePathClick("V3", mountCfg.v3) 
    end) 
    
    FLIP.MouseButton1Click:Connect(function()
        isFlipped = not isFlipped
        isFlipActive = isFlipped 
        FLIP.BackgroundColor3 = isFlipActive and FLIP_ACTIVE_COLOR or DEFAULT_COLOR
        FLIP.TextColor3 = isFlipActive and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(180, 180, 180)

        DimszyHUB16:Notify({Title = "Auto Walk", Content = isFlipped and "Flip aktif." or "Flip mati.", Duration = 1})
    end)
    
    task.spawn(function()
        local lastPlaying = false
        while task.wait(0.1) do
            if FLIP.Parent then
                FLIP.BackgroundColor3 = isFlipped and FLIP_ACTIVE_COLOR or DEFAULT_COLOR
                FLIP.TextColor3 = isFlipped and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(180, 180, 180)
            end
            
            if lastPlaying and not isPlaying then
                currentActivePath = nil
                setActivePathButtonColor(nil)
            end
            lastPlaying = isPlaying
        end
    end)

    return {
       
        Show_PLAY = function() 
            frame.Visible = true
            V1.Visible = (V1_JSON_EXISTS or false)
            V2.Visible = (V2_JSON_EXISTS or false)
            V3.Visible = (V3_JSON_EXISTS or false)
            FLIP.Visible = true
            
            if not currentActivePath then
                if V1_JSON_EXISTS then currentActivePath = "V1"
                elseif V2_JSON_EXISTS then currentActivePath = "V2"
                elseif V2_JSON_EXISTS then currentActivePath = "V3"
                else currentActivePath = nil end
            end
            
            
            
            FLIP.BackgroundColor3 = isFlipped and FLIP_ACTIVE_COLOR or DEFAULT_COLOR
            FLIP.TextColor3 = isFlipped and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(180, 180, 180)
        end,
        Hide_All = function()
            frame.Visible = false
            currentActivePath = nil 
            setActivePathButtonColor(nil)
            isFlipActive = isFlipped 
        end,
    }
end

local FloatingUI = CreateFloatingAutoWalkUI()





local function getServerLink()
    return "https://www.roblox.com/games/" .. placeId .. "/" .. jobId
end

local function rejoinServer()
    TeleportService:TeleportToPlaceInstance(placeId, jobId, player)
end
-------------------------------------------------------
-- TAB AUTO WALK (HYBRID UI)
--------------------------------------------------------

local function CreateAllTabContent() 

--TAB AUTO WALK
pcall(function()
local mainsection = Tabs.WalkTab:Section({ Title = "Auto Walk Settings" })
   
Tabs.WalkTab:Slider({
    Title = "Speed",
    Desc = "Atur kecepatan auto walk.",
    IsTooltip = true,
    IsTextbox = true,
    Step = 0.10,
    Value = {Min=0.5,Max=1,Default=1},
    Callback = function(v) playbackSpeed = v end
})

Tabs.WalkTab:Divider({ Title = "Select Mount" })

function updateControlUI() 
    for _, elem in ipairs(activeUIElements) do
        pcall(function() 
            if elem.Type == "Toggle" and elem.CurrentValue then
                stopPlayback(true) 
                elem:SetValue(false) 
            end
            if elem.Remove then elem:Remove() elseif elem.Destroy then elem:Destroy() end 
        end)
    end
    activeUIElements = {} 
    
    currentFloatingPath = nil -- <<< Tambahkan: Reset path file lengkap
    
    FloatingUI.Hide_All()
    SimpleFloatingControls.Hide() 
    stopPlayback(true)
    
    if currentMountType == "FLOATING" then
        
        DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Mengecek ketersediaan file", Duration = 1 })
        
        local mountConfig = FloatingMounts[currentMountName]
        if not mountConfig then return end

        --- START MODIFIKASI: Logika Path Cerdas
        
        -- Fungsi helper untuk menentukan full path dan base URL
        local function getMountPaths(v, v_file)
    local fullPath = ""
    local baseURL = ""
    if v and v ~= "" then
        if v_file then
            -- Kasus A: Jika v_file didefinisikan
            local fileName = v_file
            if fileName == "" then fileName = "main.json" end
            fullPath = v .. fileName
            baseURL = v 
        else
            -- Kasus B: Jika v_file TIDAK didefinisikan (v adalah path yang sebenarnya)
            
            -- ✅ PERBAIKAN 1: PRIORITAS TERTINGGI untuk path yang diakhiri .json
            if v:sub(-5) == ".json" then
                -- Jika sudah merupakan file JSON (misal: "mount_yagesya.json"), gunakan apa adanya.
                fullPath = v
                baseURL = getDirectoryPath(v)
            elseif v:sub(-1) == '/' then
                -- Jika path folder, baru tambahkan "main.json"
                fullPath = v .. "main.json"
                baseURL = v
            else
                -- Fallback lainnya, anggap sebagai path file tunggal
                fullPath = v
                baseURL = getDirectoryPath(v)
            end
        end
    end
    return fullPath, baseURL
end
        local fullPathV1, baseURLV1 = getMountPaths(mountConfig.v1, mountConfig.v1_file)
        local fullPathV2, baseURLV2 = getMountPaths(mountConfig.v2, mountConfig.v2_file)
        local fullPathV3, baseURLV3 = getMountPaths(mountConfig.v3, mountConfig.v3_file)
        
        --- END MODIFIKASI

        V1_JSON_EXISTS = false
        V2_JSON_EXISTS = false
        V3_JSON_EXISTS = false
        
        -- MODIFIKASI: Gunakan fullPathVX yang baru dihitung.
        -- Kami asumsikan CheckFileOnly telah dimodifikasi di solusi sebelumnya untuk menangani empty string.

        CheckFileOnly(fullPathV1, function(existsV1)
            V1_JSON_EXISTS = existsV1

            CheckFileOnly(fullPathV2, function(existsV2)
                V2_JSON_EXISTS = existsV2
             
            CheckFileOnly(fullPathV3, function(existsV3)
                V3_JSON_EXISTS = existsV3

                for _, elem in ipairs(activeUIElements) do
                    if elem.Type == "Button" or elem.Type == "Paragraph" then 
                        pcall(function() if elem.Remove then elem:Remove() elseif elem.Destroy then elem:Destroy() end end)
                    end
                end
                activeUIElements = {}

                local numFiles = (V1_JSON_EXISTS and 1 or 0) + (V2_JSON_EXISTS and 1 or 0) + (V3_JSON_EXISTS and 1 or 0) 

                if numFiles == 0 then
                    local paragraph = Tabs.WalkTab:Paragraph({ Title = "❌ File Tidak Ditemukan", Content = "JSON tidak tersedia" })
                    table.insert(activeUIElements, paragraph)

                elseif numFiles >= 2 then -- Gabungkan 3 dan 2 file menjadi satu bagian jika diperlukan
 
                    local title = "Start Auto Walk"
                    if numFiles == 3 then title = title .. " (Pilih versi)" end
                    if numFiles == 2 then title = title .. " (Pilih V1 atau V2)" end

                    local startBtn = Tabs.WalkTab:Button({
                        Title = title,
                        Callback = function()
                            stopPlayback(true)
                            -- Jika ada 2/3 file, biarkan FloatingUI yang menentukan baseURL & currentFloatingPath
                            -- Namun, baseURL harus diset ke path default/minimal, misalnya V1
                            baseURL = baseURLV1
                            currentFloatingPath = nil -- Biarkan FloatingUI.Show_PLAY() yang menanganinya
                            FloatingUI.Show_PLAY() 
                        end
                    })
                    table.insert(activeUIElements, startBtn)
               
                elseif numFiles == 1 then
                    
                    local startBtn = Tabs.WalkTab:Button({
                        Title = "Start Auto Walk",
                        Callback = function()
                            stopPlayback(true)
                            FloatingUI.Show_PLAY() 
                            
                            -- MODIFIKASI KRITIS: Set baseURL dan currentFloatingPath
                            if V1_JSON_EXISTS then
                                baseURL = baseURLV1
                                currentFloatingPath = fullPathV1
                            elseif V2_JSON_EXISTS then
                                baseURL = baseURLV2
                                currentFloatingPath = fullPathV2
                            elseif V3_JSON_EXISTS then
                                baseURL = baseURLV3
                                currentFloatingPath = fullPathV3
                            end
                        end
                        
                    })
                    table.insert(activeUIElements, startBtn)
                end

                -- Perbaikan: Menggunakan Tabs.WalkTab
                local stopBtn = Tabs.WalkTab:Button({
                    Title = "Stop Auto Walk",
                    Callback = function()
                        stopPlayback(true)
                        FloatingUI.Hide_All() 
                        SimpleFloatingControls.Hide()
                        DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Auto walk dihentikan.", Duration = 2 })
                    end
                })
                table.insert(activeUIElements, stopBtn)
            end)
        end)
      end)
  

    elseif currentMountType == "CHECKPOINT" then
        
        -- Perbaikan: Menggunakan Tabs.WalkTab
        local showControlsToggle = Tabs.WalkTab:Toggle({
            Title = "Show Floating Controls",
            Default = false,
            Callback = function(v)
                FloatingUI.Hide_All()
                SimpleFloatingControls.Hide()
                if v then 
                    SimpleFloatingControls.Show() 
                    DimszyHUB16:Notify({ Title = "Controls", Content = "Simple Floating Controls Aktif.", Duration = 2 })
                end
            end
        })
        table.insert(activeUIElements, showControlsToggle)


        local mData = CheckpointMounts[currentMountName]
        if mData and mData.files then
            for i, info in ipairs(mData.files) do
                -- Perbaikan: Menggunakan Tabs.WalkTab
                local tg = Tabs.WalkTab:Toggle({ 
                    Title = info.name,
                    Default = false,
                    Callback = function(v)
                        if v and showControlsToggle.CurrentValue == false then
                            showControlsToggle:SetValue(true)
                        end
                        
                        for _, otherTg in ipairs(activeUIElements) do
                            if otherTg.Type == "Toggle" and otherTg ~= tg and otherTg ~= showControlsToggle and otherTg.CurrentValue then
                                otherTg:SetValue(false)
                            end
                        end
                        
                        if not v then 
                            stopPlayback(true) 
                            return 
                        end
                        task.wait(0.05)
                        
                        playSingleCheckpointFile(info.file, i, mData.files)
                    end
                })
                table.insert(activeUIElements, tg)
            end
        end

        -- Perbaikan: Menggunakan Tabs.WalkTab
        local stopBtn = Tabs.WalkTab:Button({ 
            Title = "Stop Auto Walk",
            Callback = function()
                stopPlayback(true)
                SimpleFloatingControls.Hide()
                for _, otherTg in ipairs(activeUIElements) do
                    if otherTg.Type == "Toggle" and string.sub(otherTg.Title, 1, 1) ~= "S" and otherTg.CurrentValue then
                        otherTg:SetValue(false)
                    end
                end
                DimszyHUB16:Notify({ Title = "Auto Walk", Content = "Auto walk dihentikan.", Duration = 2 })
            end
        })
        table.insert(activeUIElements, stopBtn)
    end
end

local dropdownItems = {}
for name, _ in pairs(FloatingMounts) do table.insert(dropdownItems, name) end
for name, _ in pairs(CheckpointMounts) do table.insert(dropdownItems, name) end
table.sort(dropdownItems)

Tabs.WalkTab:Dropdown({
    Title = "Pilih Jenis Mount",
    Values = dropdownItems,
    Callback = function(selectedMount)
        currentMountName = selectedMount
        
        if FloatingMounts[selectedMount] then
            currentMountType = "FLOATING"
            baseURL = FloatingMounts[selectedMount].v1
        elseif CheckpointMounts[selectedMount] then
            currentMountType = "CHECKPOINT"
            baseURL = CheckpointMounts[selectedMount].path
        end
        
        -- Tambahkan notifikasi di sini
        DimszyHUB16:Notify({ 
            Title = "Mount Dipilih", 
            Content = "Mount " .. currentMountName .. " telah diatur.", 
            Duration = 1.5 
        })

        stopPlayback(true)
        updateControlUI() 
    end
})
end)


 --  Main Tab
pcall(function() 
Tabs.MainTab:Section({ Title = "Server Info", TextSize = 20 })
Tabs.MainTab:Divider()

local placeName = "Unknown"
local success, productInfo = pcall(function()
    return MarketplaceService:GetProductInfo(placeId)
end)
if success and productInfo then
    placeName = productInfo.Name
end

Tabs.MainTab:Paragraph({
    Title = "Game Mode",
    Desc = placeName
})

Tabs.MainTab:Button({
    Title = "Copy Server Link",
    Desc = "Copy the current server's join link",
    Icon = "link",
    Callback = function()
        local serverLink = getServerLink()
        pcall(function()
            setclipboard(serverLink)
        end)
        DimszyHUB16:Notify({
            Icon = "link",
            Title = "Link Copied",
            Content = "The server invite link has been copied to your clipboard",
            Duration = 3
        })
    end
})

local numPlayers = #Players:GetPlayers()
local maxPlayers = Players.MaxPlayers

Tabs.MainTab:Paragraph({
    Title = "Current Players",
    Desc = numPlayers .. " / " .. maxPlayers
})

Tabs.MainTab:Paragraph({
    Title = "Server ID",
    Desc = jobId
})

Tabs.MainTab:Paragraph({
    Title = "Place ID",
    Desc = tostring(placeId)
})

Tabs.MainTab:Section({ Title = "Server Tools", TextSize = 20 })
Tabs.MainTab:Divider()

Tabs.MainTab:Button({
    Title = "Rejoin",
    Desc = "Rejoin the current place",
    Icon = "refresh-cw",
    Callback = function()
        rejoinServer()
    end
})

--Fungsi Find Server
local PlaceId = game.PlaceId
local function FetchServers()
    local Cursor = nil
    local Servers = {}
    repeat
        local URL = "https://games.roblox.com/v1/games/" .. tostring(PlaceId) .. "/servers/Public?sortOrder=Asc&limit=100"
        if Cursor then URL = URL .. "&cursor=" .. Cursor end
        local ok, Response = pcall(function() return game:HttpGet(URL) end)
        if not ok or not Response then break end
        local ok2, Data = pcall(function() return HttpService:JSONDecode(Response) end)
        if ok2 and Data and Data.data then for _, server in ipairs(Data.data) do table.insert(Servers, server) end end
        if ok2 and Data then Cursor = Data.nextPageCursor else Cursor = nil end
        task.wait(0.3)
    until Cursor == nil
    return Servers
end
local function CreateServerButtons()
    local targetTab = Tabs.MainTab
    if targetTab.Clear then pcall(function() targetTab:Clear() end) end
    local Loading = targetTab:Paragraph({ Title = "🔍 Mencari Server...", Content = "Mengambil data server..." })
    local allServers = FetchServers()
    pcall(function() Loading:Set("Content", "") end)
    local ListSection = targetTab:Section({ Title = "Server Result" })
    if #allServers == 0 then ListSection:Paragraph({ Title = "❌ Tidak ada server!", Content = "API mungkin down." }) return end
    for _, server in ipairs(allServers) do
        local playing = tonumber(server.playing) or 0
        local maxPlayers = tonumber(server.maxPlayers) or 1
        local isSafe = playing <= (maxPlayers / 2)
        local emoji = isSafe and "🟢" or "🟥"
        local name = string.format("%s Server [%s/%s] - %s", emoji, playing, maxPlayers, isSafe and "Safe" or "No Safe")
        ListSection:Button({
            Title = name,
            Callback = function() game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceId, server.id) end
        })
    end
end

Tabs.MainTab:Button({
    Title = "Find Server",
    Desc = "Finding a Server inside your game",
    Icon = "server",
    Callback = function()
        CreateServerButtons() 
    end
})
end)


pcall(function() 
Tabs.SettingsTab:Section({ Title = "Settings", TextSize = 40 })
Tabs.SettingsTab:Section({ Title = "Personalize", TextSize = 20 })
Tabs.SettingsTab:Divider()

local themes = {}
for themeName, _ in pairs(DimszyHUB16:GetThemes()) do
    table.insert(themes, themeName)
end
table.sort(themes)

local canChangeTheme = true
local canChangeDropdown = true

local ThemeDropdown = Tabs.SettingsTab:Dropdown({
    Title = "THEME_SELECT",
    Values = themes,
    SearchBarEnabled = true,
    MenuWidth = 280,
    Value = "true",
    Callback = function(theme)
        if canChangeDropdown then
            canChangeTheme = false
            DimszyHUB16:SetTheme(theme)
            canChangeTheme = true
        end
    end
})

local TransparencySlider = Tabs.SettingsTab:Slider({
    Title = "TRANSPARENCY",
    IsTooltip = true,
    IsTextbox = true,
    Value = { Min = 0, Max = 1, Default = 0.2, Step = 0.1 },
    Callback = function(value)
        DimszyHUB16.TransparencyValue = tonumber(value)
        Window:ToggleTransparency(tonumber(value) > 0)
    end
})

local ThemeToggle = Tabs.SettingsTab:Toggle({
    Title = "Enable Dark Mode",
    Desc = "Use dark color theme",
    Value = false,
    Callback = function(state)
        if canChangeTheme then
            local newTheme = state and "true" or "true"
            DimszyHUB16:SetTheme(newTheme)
            if canChangeDropdown then
                ThemeDropdown:Select(newTheme)
            end
        end
    end
})

DimszyHUB16:OnThemeChange(function(theme)
    canChangeTheme = false
    ThemeToggle:Set(theme == "true")
    canChangeTheme = true
end)

Tabs.SettingsTab:Section({ Title = "Keybind Settings", TextSize = 20 })
Tabs.SettingsTab:Section({ Title = "Change toggle key for GUI", TextSize = 16, TextTransparency = 0.25 })
Tabs.SettingsTab:Divider()

Tabs.SettingsTab:Keybind({
    Flag = "keybind ui toggles",
    Title = "Keybind",
    Desc = "Keybind to open ui",
    Value = initialKeyName,
    Callback = function(v)
        local keyCode = Enum.KeyCode[v]
        Window:SetToggleKey(keyCode)
        saveKeybind(keyCode)
    end
})



end) 
end

         
-- =====================================================
-- FINAL KEY SYSTEM + GLOBAL EXPIRE (10 RANDOM KEYS)
-- =====================================================

_G.KEY_UNLOCKED = false
local typedToken = ""

-- =====================================================
-- 🔑 DAFTAR KEY (10 KEY RANDOM)
-- =====================================================
local VALID_KEYS = {
    "FREE-AX92Q",
    "FREE-K9P2M",
    "FREE-ZX81L",
    "FREE-MN72Q",
    "FREE-PL09X",
    "FREE-QW88A",
    "FREE-19LMZ",
    "FREE-XP7AA",
    "FREE-0QWNM",
    "FREE-LA72P"
}

local function ValidateToken(token)
    for _, key in ipairs(VALID_KEYS) do
        if token == key then
            return true
        end
    end
    return false
end

-- =====================================================
-- ⏰ GLOBAL EXPIRE TIME (SEMUA ORANG)
-- =====================================================
local GLOBAL_EXPIRE_TIME = os.time({
    year = 2026,
    month = 2,
    day = 7,
    hour = 23,
    min = 59,
    sec = 59
})

-- =====================================================
-- ❌ CEK EXPIRE DI AWAL
-- =====================================================
if os.time() > GLOBAL_EXPIRE_TIME then
    game.Players.LocalPlayer:Kick("Script expired! Masa akses sudah habis.")
    return
end

-- =====================================================
-- 🔐 KEY SYSTEM TAB
-- =====================================================
local KeyTab = Window:Tab({
    Title = "KEY SYSTEM LOGIN",
    Icon = "lock"
})

KeyTab:Input({
    Title = "Masukkan Key",
    Placeholder = "Paste key disini...",
    Callback = function(v)
        typedToken = v
    end
})

KeyTab:Button({
    Title = "🔐 Verify Key",
    Callback = function()

        if typedToken == "" then
            return DimszyHUB16:Notify({
                Title = "Key",
                Content = "Key tidak boleh kosong!",
                Duration = 3
            })
        end

        if os.time() > GLOBAL_EXPIRE_TIME then
            game.Players.LocalPlayer:Kick("Script expired! Masa akses sudah habis.")
            return
        end

        if ValidateToken(typedToken) then
            _G.KEY_UNLOCKED = true

            Tabs.MainTab = Window:Tab({ Title = "MAIN SERVER", Icon = "globe" })
            Tabs.WalkTab = Window:Tab({ Title = "AUTO WALK", Icon = "file" })
            Tabs.RunAnimationTab = Window:Tab({ Title = "ANIMATION", Icon = "braces" })
            Tabs.SettingsTab = Window:Tab({ Title = "SETTINGS", Icon = "settings" })

            CreateAllTabContent()
            Window:SelectTab(2)
            KeyTab.Locked = true

            DimszyHUB16:Notify({
                Title = "SUCCESS",
                Content = "Key valid! Script aktif.",
                Duration = 3
            })
        else
            game.Players.LocalPlayer:Kick("Key salah! Akses ditolak.")
        end
    end
})

Window:SelectTab(1)

-- =====================================================
-- ⛔ ANTI DIEM (CEK EXPIRE TERUS)
-- =====================================================
task.spawn(function()
    while true do
        task.wait(5)
        if _G.KEY_UNLOCKED and os.time() > GLOBAL_EXPIRE_TIME then
            game.Players.LocalPlayer:Kick("Script expired! Masa akses sudah habis.")
        end
    end
end)
