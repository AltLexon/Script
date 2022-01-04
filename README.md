local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/GreenDeno/Venyx-UI-Library/main/source.lua"))()
local lib = library.new("Legends Of Speed")

local plr = game.Players.LocalPlayer
_G.autoFarm = false
local ORBEVENT = game.ReplicatedStorage.rEvents.orbEvent

-- pagina 1 --
local pagina1 = lib:addPage("Farm", 1)
local section1 = pagina1:addSection("Player")
local section2 = pagina1:addSection("Farm")
local section5 = pagina1:addSection("Races")
local section3 = pagina1:addSection("Misc")

section1:addSlider("WalkSpeed",16,16,3000,function (value)
    plr.Character.Humanoid.WalkSpeed = value
end)
section1:addSlider("JumpPower",50,50,300,function (value)
    plr.Character.Humanoid.JumpPower = value
end)
section1:addTextbox("Local Name","",function (value)
    plr.DisplayName = value
    print("its name has been changed to:", value)
end)
section2:addToggle("Steps",false,function (bool)
    _G.autoFarm = bool
    if bool then
        Steps();
    end
end)
section2:addToggle("Rebirths",false,function (bool)
    _G.autoFarm = bool
    if bool then
        Rebirth();
    end
end)
section2:addToggle("Gems",false,function (bool)
    _G.autoFarm = bool
    if bool then
        Gems();
    end
end)
section2:addToggle("Hoops",false,function (bool)
    _G.autoFarm = bool
    if bool then
        Hoops();
    end
end)
section3:addButton("By AltLexon#7185",function(v)
    setclipboard("AltLexon#7185")
end)
section3:addButton("PlaceId", function (value)
    print("PlaceId:", tostring(game.PlaceId))
    wait(1)
    print("Copied in 3")
    wait(1)
    print("Copied in 2")
    wait(1)
    print("Copied in 1")
    wait(1)
    print("PlaceId Copied!")
    setclipboard(tostring(game.PlaceId))
end)
section5:addDropdown("Select", {"Grassland", "Desert", "Magma"},function (v)
    game.Workspace.raceMaps[v].boundaryParts:Destroy()
end)
section5:addButton("TP End: Grassland",function ()
    plr.Character.HumanoidRootPart.CFrame = CFrame.new(1686.07495, 36.3147125, -5946.63428, -0.984812617, 0, 0.173621148, 0, 1, 0, -0.173621148, 0, -0.984812617)
end)
section5:addButton("TP End: Desert",function ()
    plr.Character.HumanoidRootPart.CFrame = CFrame.new(48.3109131, 36.3147125, -8680.45312, -1, 0, 0, 0, 1, 0, 0, 0, -1)
end)
section5:addButton("TP End: Magma   ",function ()
    plr.Character.HumanoidRootPart.CFrame = CFrame.new(1001.33118, 36.3147125, -10986.2178, -0.996191859, 0, -0.0871884301, 0, 1, 0, 0.0871884301, 0, -0.996191859)
end)

-- functions --
-- pagina 1 --
function Steps()
    spawn(function ()
        while _G.autoFarm == true do
        ORBEVENT:FireServer("collectOrb", "Red Orb", "City")
        ORBEVENT:FireServer("collectOrb", "Red Orb", "City")
        ORBEVENT:FireServer("collectOrb", "Red Orb", "City")
        ORBEVENT:FireServer("collectOrb", "Red Orb", "City")
        ORBEVENT:FireServer("collectOrb", "Red Orb", "City")
            wait()
        end
    end)
end
function Gems()
    spawn(function ()
        while _G.autoFarm == true do
        ORBEVENT:FireServer("collectOrb", "Gem", "City")
        ORBEVENT:FireServer("collectOrb", "Gem", "City")
        ORBEVENT:FireServer("collectOrb", "Gem", "City")
        ORBEVENT:FireServer("collectOrb", "Gem", "City")
        ORBEVENT:FireServer("collectOrb", "Gem", "City")
            wait()
        end
    end)
end
function Hoops()
    spawn(function ()
        while _G.autoFarm == true do
            local oldcframe = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
            for _,v in pairs(game:GetService("Workspace").Hoops:GetChildren()) do
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.CFrame
                wait(0.1)
            end
            wait(0.1)
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcframe
            wait(8)
        end
    end)
end
function Rebirth()
    spawn(function ()
        while _G.autoFarm == true do
        local A_1 = "rebirthRequest"
        local Event = game:GetService("ReplicatedStorage").rEvents.rebirthEvent
        Event:FireServer(A_1)
            wait(8)
        end
    end)
end
-- pagina 2 --
local pagina2 = lib:addPage("Settings")
local colors = pagina2:addSection("Colors")
local section4 = pagina2:addSection("Others")


local themes = {
	Background = Color3.fromRGB(24, 24, 24),
	Glow = Color3.fromRGB(0, 0, 0),
	Accent = Color3.fromRGB(10, 10, 10),
	LightContrast = Color3.fromRGB(20, 20, 20),
	DarkContrast = Color3.fromRGB(14, 14, 14),  
	TextColor = Color3.fromRGB(255, 255, 255)
}


for theme, color in pairs(themes) do
	colors:addColorPicker(theme, color, function(color3)
		lib:setTheme(theme, color3)
	end)
end

section4:addKeybind("Toggle UI", Enum.KeyCode.RightControl,function ()
    lib:toggle()
end)

lib:SelectPages(lib.pages[1], true)
