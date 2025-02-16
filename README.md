local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "🗒️ Universal Script 🗒️",
   Icon = 0, -- Icon in Topbar. Can use Lucide Icons (string) or Roblox Image (number). 0 to use no icon (default).
   LoadingTitle = "Universal Script!",
   LoadingSubtitle = "Created By Ronaldo_H55",
   Theme = "Amethyst", -- Check https://docs.sirius.menu/rayfield/configuration/themes

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false, -- Prevents Rayfield from warning when the script has a version mismatch with the interface

   ConfigurationSaving = {
      Enabled = false,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "File example"
   },

   Discord = {
      Enabled = True, -- Prompt the user to join your Discord server if their executor supports it
      Invite = "noinvitelink", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ ABCD would be ABCD
      RememberJoins = true -- Set this to false to make them join the discord every time they load it up
   },

   KeySystem = true, -- Set this to true to use our key system
   KeySettings = {
      Title = "Universal | Key",
      Subtitle = "Link In Discord Server",
      Note = "Join Server From Misc Tab", -- Use this to tell the user how to get a key
      FileName = "ExampleFileName", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = True , -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"RonaldoIsProbablyTheGoat"} -- List of keys that will be accepted by the system, can be RAW file links (pastebin, github etc) or simple strings ("hello","key22")
   }
}) 

local MainTab = Window:CreateTab("🏡 Home", nil) -- Title, Image
local MainSection = MainTab:CreateSection("Main")

Rayfield:Notify({
   Title = "You executed the script successfully!",
   Content = "[UPDATED AND WORKING 100%]",
   Duration = 7,
   Image = nil,
})

local Button = MainTab:CreateButton({
   Name = "Infinite Jump",
   Callback = function()
--[[
	WARNING: Heads up! This script has not been verified by ScriptBlox. Use at your own risk!
]]
local InfiniteJumpEnabled = true
game:GetService("UserInputService").JumpRequest:connect(function()
	if InfiniteJumpEnabled then
		game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")
	end
end)
   end,
})

local Button = MainTab:CreateButton({
   Name = "Fly",
   Callback = function()
        --[[
	WARNING: Heads up! This script has not been verified by ScriptBlox. Use at your own risk!
]]
loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
   end,
})

local Slider = MainTab:CreateSlider({
   Name = "WalkSpeed",
   Range = {16, 700},
   Increment = 1,
   Suffix = "Speed",
   CurrentValue = 16,
   Flag = "Slider1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = (Value)
   end,
})

local Slider = MainTab:CreateSlider({
   Name = "JumpPower",
   Range = {0, 200},
   Increment = 1,
   Suffix = "JumpPower",
   CurrentValue = 0,
   Flag = "Slider1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = (Value)
   end,
})

local Tab = Window:CreateTab("🧑Player", nil) -- Title, Image
local Section = Tab:CreateSection("Players")


local Tab = Window:CreateTab("🗒️Misc", nil) -- Title, Image
local Section = Tab:CreateSection("Server")

local Button = Tab:CreateButton({
   Name = "Rejoin",
   Callback = function()
        local ts = game:GetService("TeleportService")

local p = game:GetService("Players").LocalPlayer



ts:TeleportToPlaceInstance(game.PlaceId, game.JobId, p)
   end,
})

local Divider = Tab:CreateDivider()

local Button = Tab:CreateButton({
   Name = "Destroy",
   Callback = function()
Rayfield:Destroy()
   end,
})

local Button = Tab:CreateButton({
   Name = "Infinity Yield",
   Callback = function()
loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))()
   end,
})

local Divider = Tab:CreateDivider()

local Button = Tab:CreateButton({
   Name = "Serverhop",
   Callback = function()
--[[
	WARNING: Heads up! This script has not been verified by ScriptBlox. Use at your own risk!
]]
local PlaceID = game.PlaceId
local AllIDs = {}
local foundAnything = ""
local actualHour = os.date("!*t").hour
local Deleted = false
local File = pcall(function()
    AllIDs = game:GetService('HttpService'):JSONDecode(readfile("NotSameServers.json"))
end)
if not File then
    table.insert(AllIDs, actualHour)
    writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
end
function TPReturner()
    local Site;
    if foundAnything == "" then
        Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
    else
        Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
    end
    local ID = ""
    if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
        foundAnything = Site.nextPageCursor
    end
    local num = 0;
    for i,v in pairs(Site.data) do
        local Possible = true
        ID = tostring(v.id)
        if tonumber(v.maxPlayers) > tonumber(v.playing) then
            for _,Existing in pairs(AllIDs) do
                if num ~= 0 then
                    if ID == tostring(Existing) then
                        Possible = false
                    end
                else
                    if tonumber(actualHour) ~= tonumber(Existing) then
                        local delFile = pcall(function()
                            delfile("NotSameServers.json")
                            AllIDs = {}
                            table.insert(AllIDs, actualHour)
                        end)
                    end
                end
                num = num + 1
            end
            if Possible == true then
                table.insert(AllIDs, ID)
                wait()
                pcall(function()
                    writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
                    wait()
                    game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
                end)
                wait(4)
            end
        end
    end
end

function Teleport()
    while wait() do
        pcall(function()
            TPReturner()
            if foundAnything ~= "" then
                TPReturner()
            end
        end)
    end
end

-- If you'd like to use a script before server hopping (Like a Automatic Chest collector you can put the Teleport() after it collected everything.
Teleport()
   end,
})

local Button = Tab:CreateButton({
   Name = "QuizBot {WARNING: This will delete the script}",
   Callback = function()
local CategoryManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/Damian-11/quizbot/master/quizbot.luau"))()
   end,
})
