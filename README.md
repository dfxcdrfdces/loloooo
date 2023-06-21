local bindable
local lr = game.ReplicatedStorage.GameData.LatestRoom
 
local function GetCurrentRoom()
    return workspace.CurrentRooms:WaitForChild(tostring(lr.Value + 1), 5)
end
 
local function Convert(room)
    local noder = room:WaitForChild("PathfindNodes", 2):Clone()
    noder.Parent = room
    noder.Name = "Nodes"
 
    local Goober = Instance.new("StringValue", room)
    Goober.Name = "gobble ur balls L splash"
    Goober.Value = "seriously do it now loser"
 
    warn("Converted "..room.Name.." to support node system")
 
    local A = room:WaitForChild("RoomEntrance", .5):Clone()
    A.Parent = room
    A.Name = "RoomStart"
 
    local B = room:WaitForChild("RoomExit", .5):Clone()
    B.Parent = room
    B.Name = "RoomEnd"
end
 
bindable = workspace.CurrentRooms.ChildAdded:Connect(function()
    local room = GetCurrentRoom()
    Convert(room)
end)
 
Convert(GetCurrentRoom())
 
warn("Executed entity fixer, made by that one crow man who also happens to possess a gun lol")




local Beans = false
local Bravo = false
local LightReplaceModel = game:GetObjects("rbxassetid://12543866876")[1] or nil
local BookcaseReplaceModel = nil
local v8 = game:GetService("ReplicatedStorage").Sounds:FindFirstChild("LA_The Garden");
function PreloadSounds(msg,Soundid)
	if not game:GetService("ReplicatedStorage").Sounds:FindFirstChild("LA_"..msg) then
		Sound = v8:Clone()
		Sound.SoundId = Soundid
		Sound.Parent = game:GetService("ReplicatedStorage").Sounds
		Sound.Name ='LA_'..msg
	end
end
print("Loade")
game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Game.Health.Music.Blue.SoundId = "rbxassetid://10472612727"
game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Game.Health.Music.Blue.Pitch = 0.55

game.Lighting.FogColor = Color3.fromRGB(0, 0, 0)
game.Lighting.FogStart = 5
game.Lighting.FogEnd = 800

game.ReplicatedStorage.Sounds.BulbZap.SoundId = "rbxassetid://4398878054"

local latestroom = game.ReplicatedStorage.GameData.LatestRoom.Value
local roomlatestworkspace = workspace.CurrentRooms[latestroom]

function changedoormaterial(doormodel)
	doormodel.Door.Material = "DiamondPlate"
	doormodel.Door.Color = Color3.fromRGB(80,80,80)

	doormodel.Door.Sign.Material = "Metal"
	doormodel.Door.Sign.Color = Color3.fromRGB(111,111,111)

	doormodel.Sign.Stinker.TextColor3 = Color3.new(0.8,0.8,0.8)
	doormodel.Sign.Stinker.Highlight.TextColor3 = Color3.new(0.6,0.6,0.6)
end
function message2(msg,SoundId)
	PreloadSounds(msg,SoundId)
	gameid = game.PlaceId
	Length = Length or 5
	if (gameid==6839171747) then
		game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Game.Reminder.Enabled=true
		M = require(game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Game)
	elseif (gameid == 6516141723) then
		game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Lobby.Reminder.Enabled=true
		M = require(game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Lobby)
	end    
	M.titlelocation(msg) -- Text,Enabled,Length
end

function ChangeStyle(room,Modifed)
	Modifed=Modifed or 'Idk'
	wait(0)
	if Modifed == 'Chandelier' then
		for i,v in pairs(room.Assets:GetDescendants()) do
			if v.Name == "Chandelier" then
				v:Destroy()
			end
		end
		return
	end
	--Change Light Model
	for i,v in pairs(room.Assets.Light_Fixtures:GetDescendants()) do
		if v.Name == "LightStand" then
			if game.ReplicatedStorage.GameData.LatestRoom.Value < 51 then
				local torch = LightReplaceModel:Clone()
				torch.Parent = room.Assets.Light_Fixtures
				torch.LightFixture.PointLight.Changed:Connect(function()
					torch.LightFixture.Neon.atachm["Ok you cannot tell me this isnt good"].Enabled = torch.LightFixture.PointLight.Enabled
					torch.LightFixture.Neon["Bright sh idfk"].ParticleEmitter.Enabled = torch.LightFixture.PointLight.Enabled
					torch.LightFixture:WaitForChild('Dust').ParticleEmitter.Enabled = torch.LightFixture.PointLight.Enabled
				end)
				torch:PivotTo(v:GetPivot())
				v:Destroy()
			else
				v:Destroy()
			end
		end
	end
	--FUNCTIONEND
end

--Change Seek Eye Model
for i,v in pairs(game.ReplicatedStorage.Misc.Eyes:GetDescendants()) do
	if v.Name == "Eye" then
		v:FindFirstChild("Part").Decal.Texture = "rbxassetid://1882220622"
		v:FindFirstChild("Eye").Name = "KYS"
	end
end

--Change Currentroom
ChangeStyle(roomlatestworkspace)


spawn(function()
	game.ReplicatedStorage.GameData.LatestRoom.Changed:Wait()
	print("Something much more deeper has begun.")
end)


--CHange latest room on value change

game.ReplicatedStorage.GameData.LatestRoom.Changed:Connect(function(v)
	if v > 52 or Bravo then
		ChangeStyle(workspace.CurrentRooms[game.ReplicatedStorage.GameData.LatestRoom.Value],'Chandelier') 
	end

	if v == 49 then
		message2('figures ass','rbxassetid://1835274270')
	elseif v > 64 and workspace.CurrentRooms[v]:FindFirstChild('Assets'):FindFirstChild('Bed_Infirmary') and v < 80  then
		Sound = GetGitSoundID("https://github.com/Sosnen/Ping-s-Dumbass-projects-/blob/main/Ambience_Infirmary_Entrence.mp3?raw=true",'infermy')
		message2('The fucking among us imfirrjd',Sound)
	elseif v > 80 and workspace.CurrentRooms[v]:FindFirstChild('Assets'):FindFirstChild('Garden_LanternUnique') and v < 99  then
		message2('The Grass Touch','rbxassetid://7132953277')
	end
	if v == 53 then
		Sound = GetGitSoundID("https://github.com/Sosnen/Ping-s-Dumbass-projects-/blob/main/Dark-Depths_Entrencebetter.mp3?raw=true",'dork')
		message2('The Fatass rooms',Sound)
		Bravo=true
		Beans = true
	elseif v == 90 then
		message2('The Dark ass house','rbxassetid://1847269119')
	elseif v == 100  then
		message2('Figures Sex Dungeon','rbxassetid://1837449237')
	end
	local latestroom = game.ReplicatedStorage.GameData.LatestRoom.Value
	local roomlatestworkspace = workspace.CurrentRooms[latestroom]

	ChangeStyle(roomlatestworkspace)


end)

--Bravo 6, going dark.

workspace.Ambience_Dark.Played:Connect(function()
	Bravo = true
	wait(.01)
	workspace.CurrentRooms[game.ReplicatedStorage.GameData.LatestRoom.Value].Assets.Light_Fixtures:Destroy()
	--workspace.CurrentRooms[game.ReplicatedStorage.GameData.LatestRoom.Value].Assets.Chandelier:Destroy()
	workspace.Ambience_Dark:Stop()
	game.Lighting.FogStart = 10
	game.Lighting.FogEnd = 10000000
end)


--sprint, pls follow the instructions if u wanna change your keybinds (default is Q)
local Parent = game.Players.LocalPlayer.PlayerGui

local Sprint = Instance.new("Frame")
local ImageLabel = Instance.new("ImageLabel")
local UICorner = Instance.new("UICorner")
local UIPadding = Instance.new("UIPadding")
local Bar = Instance.new("Frame")
local UICorner_2 = Instance.new("UICorner")
local UIPadding_2 = Instance.new("UIPadding")
local Fill = Instance.new("Frame")
local UICorner_3 = Instance.new("UICorner")

--Properties:

local StaminaGui = Instance.new("ScreenGui")

--Properties:

StaminaGui.Name = "StaminaGui"
StaminaGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
StaminaGui.Enabled = true -- Want hell mode? Yea?? Set this to false then, and enjoy suffering
StaminaGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

Sprint.Name = "Sprint"
Sprint.Parent = StaminaGui
Sprint.AnchorPoint = Vector2.new(0, 1)
Sprint.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Sprint.BackgroundTransparency = 1.000
Sprint.Position = UDim2.new(0.931555569, 0, 0.987179458, 0)
Sprint.Size = UDim2.new(0.0556001104, 0, 0.0756410286, 0)
Sprint.SizeConstraint = Enum.SizeConstraint.RelativeYY
Sprint.ZIndex = 1005

ImageLabel.Parent = Sprint
ImageLabel.BackgroundColor3 = Color3.fromRGB(255, 222, 189)
ImageLabel.Size = UDim2.new(1, 0, 1, 0)
ImageLabel.SizeConstraint = Enum.SizeConstraint.RelativeYY
ImageLabel.Visible = false

UICorner.CornerRadius = UDim.new(1, 0)
UICorner.Parent = ImageLabel

UIPadding.Parent = Sprint
UIPadding.PaddingBottom = UDim.new(0.300000012, -5)
UIPadding.PaddingLeft = UDim.new(0.0199999996, 0)
UIPadding.PaddingRight = UDim.new(0.0500000007, -15)
UIPadding.PaddingTop = UDim.new(0.300000012, -5)

Bar.Name = "Bar"
Bar.Parent = Sprint
Bar.AnchorPoint = Vector2.new(0, 0.5)
Bar.BackgroundColor3 = Color3.fromRGB(56, 46, 39)
Bar.BackgroundTransparency = 0.700
Bar.Position = UDim2.new(-2.72600269, 0, 0.499999672, 0)
Bar.Size = UDim2.new(3.60599804, 0, 0.600000083, 0)
Bar.ZIndex = 0

UICorner_2.CornerRadius = UDim.new(0.25, 0)
UICorner_2.Parent = Bar

UIPadding_2.Parent = Bar
UIPadding_2.PaddingBottom = UDim.new(0, 4)
UIPadding_2.PaddingLeft = UDim.new(0, 4)
UIPadding_2.PaddingRight = UDim.new(0, 4)
UIPadding_2.PaddingTop = UDim.new(0, 4)

Fill.Name = "Fill"
Fill.Parent = Bar
Fill.AnchorPoint = Vector2.new(0, 0.5)
Fill.BackgroundColor3 = Color3.fromRGB(213, 185, 158)
Fill.Position = UDim2.new(0, 0, 0.5, 0)
Fill.Size = UDim2.new(1, 0, 1, 0)
Fill.ZIndex = 2

UICorner_3.CornerRadius = UDim.new(0.25, 0)
UICorner_3.Parent = Fill

local erm = Instance.new("ScreenGui")
local ImageLabel = Instance.new("ImageLabel")
erm.IgnoreGuiInset = true
erm.Name = "erm"
erm.Parent = Parent
erm.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

ImageLabel.Parent = erm
ImageLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ImageLabel.BackgroundTransparency = 1.000
ImageLabel.Size = UDim2.new(1, 0, 0.998717964, 0)
ImageLabel.Image = "rbxassetid://190596490"
ImageLabel.ImageColor3 = Color3.fromRGB(0, 0, 0)

ImageLabel.ImageTransparency = 1

-- Services

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")

-- Variables

local Plr = Players.LocalPlayer
local Char = Plr.Character or Plr.CharacterAdded:Wait()
local Hum = Char:WaitForChild("Humanoid")

local stamina, staminaMax = 100, 100
local sprintTime = 7
local cooldown = false

local ModuleScripts = {
	MainGame = require(Plr.PlayerGui.MainUI.Initiator.Main_Game),
}

-- Setup

local nIdx; nIdx = hookmetamethod(game, "__newindex", newcclosure(function(t, k, v)
	if k == "WalkSpeed" then
		if ModuleScripts.MainGame.chase then
			v = ModuleScripts.MainGame.crouching and 15 or 22
		elseif ModuleScripts.MainGame.crouching then
			v = 8
		else
			v = isSprinting and 20 or 12
		end
	end

	return nIdx(t, k, v)
end))

-- Scripts

sprintTime = math.max(sprintTime - 1, 1)
local zerostamtween = game.TweenService:Create(ImageLabel,TweenInfo.new(12),{ImageTransparency = 0})
UIS.InputBegan:Connect(function(key, gameProcessed)
	if not gameProcessed and key.KeyCode == Enum.KeyCode.Q and not cooldown and not ModuleScripts.MainGame.crouching then
		-- Sprinting

		isSprinting = true
		Hum:SetAttribute("SpeedBoost",4)
		zerostamtween:Play()
		while UIS:IsKeyDown(Enum.KeyCode.Q) and stamina > 0 do ---change Q to whatever you want your keybind to be
			stamina = math.max(stamina - 1, 0)
			Fill.Size = UDim2.new(1 / staminaMax * stamina, 1, 1, 0)
			task.wait(sprintTime / 100)

		end

		-- Reset
		zerostamtween:Pause()
		isSprinting = false
		Hum:SetAttribute("SpeedBoost",0)
		game.TweenService:Create(ImageLabel,TweenInfo.new(1),{ImageTransparency = 1}):Play()
		Hum.WalkSpeed = 12

		if stamina == 0 then
			-- Cooldown
			firesignal(game.ReplicatedStorage.EntityInfo.Caption.OnClientEvent,"You're exhausted.")
			local noStamernaSound = Instance.new("Sound",workspace)
			noStamernaSound.SoundId = "rbxassetid://8258601891"
			noStamernaSound.Volume = 0.8
			noStamernaSound.PlayOnRemove = true
			noStamernaSound:Destroy()
			cooldown = true
			game.TweenService:Create(ImageLabel,TweenInfo.new(0.3),{ImageTransparency = 0}):Play()
			wait(0.3)
			game.TweenService:Create(ImageLabel,TweenInfo.new(10),{ImageTransparency = 1}):Play()
			for i = 1, staminaMax, 1 do
				stamina = i
				Fill.Size = UDim2.new(1 / staminaMax * i, 1, 1, 0)

				task.wait(sprintTime / 50)
			end

			cooldown = false
		else
			-- Refill
			cooldown = false
			Spawn(function()
				--wait(1)
				cooldown = false
			end)
			game.TweenService:Create(ImageLabel,TweenInfo.new(1),{ImageTransparency = 1}):Play()
			while not UIS:IsKeyDown(Enum.KeyCode.Q) do ---change Q to whatever you want your keybind to be
				stamina = math.min(stamina + 1, staminaMax)
				Fill.Size = UDim2.new(1 / staminaMax * stamina, 1, 1, 0)

				task.wait(sprintTime / 50)
			end
		end        
	end
end)
Hum:SetAttribute("SpeedBoost",0)
Hum.WalkSpeed = 12
local VitaminsActivatedConnection, VitaminsDebounce = nil, false

Char.ChildAdded:Connect(function(CA)
	if CA.Name == "Vitamins" then
		local Tool = Char:FindFirstChild("Vitamins")

		VitaminsActivatedConnection = Tool.Activated:Connect(function()
			if VitaminsDebounce then
				return false
			end

			VitaminsDebounce = true

			Char.Humanoid.Health = Char.Humanoid.Health + 30

			stamina = 100

			task.delay(10, function()
				VitaminsDebounce = false
			end)
		end)

		Tool.Unequipped:Connect(function()
			VitaminsActivatedConnection:Disconnect()

			print("test")
		end)
	end
end)
--mommy im scared






game.ReplicatedStorage.GameData.LatestRoom.Changed:Connect(function()
	wait(3.5)
	if not workspace:FindFirstChild("SeekMoving") then
		return 
	end
	local RealSeek = workspace:FindFirstChild("SeekMoving")
	local RealSeekRig = RealSeek:FindFirstChild("SeekRig")
	local seekNew = game:GetObjects("rbxassetid://11664451634")[1] 
	seekNew.Name = "seek2"

	for i,v in pairs(seekNew.Figure:GetChildren()) do
		if v:IsA("Sound") then
			v:Stop()
		end
	end
	RealSeekRig.Head.Eye:Destroy()
	RealSeekRig.Head.Black:Destroy()
	seekNew.Parent = workspace
	local SeekRig = seekNew:FindFirstChild("SeekRig")
	SeekRig:FindFirstChild("Root").Anchored = true
	spawn(function()
		while game["Run Service"].Heartbeat:Wait() and RealSeek do
			if RealSeekRig:FindFirstChild("Root") then
				SeekRig:FindFirstChild("Root").CFrame = RealSeekRig:FindFirstChild("Root").CFrame
			end
			for i,v in pairs(RealSeek.Figure:GetChildren()) do
				RealSeek.Figure.Footsteps:Stop()
				RealSeek.Figure.FootstepsFar:Stop()
			end
			for i,v in pairs(RealSeekRig:GetChildren()) do
				if v:IsA("BasePart") then
					v.Transparency = 1
				end
			end
		end
	end)

	local seksound = workspace.Ambience_Seek
	seksound.Played:Connect(function()
		spawn(function()
			wait(7)
			local figure = seekNew.Figure
			figure.FootseptsFar:Play()
			figure.Footsteps:Play()
			figure.Splashing:Play()
			figure["Splashing Far"]:Play()
		end)
		local raiser = SeekRig.AnimationController:LoadAnimation(SeekRig.AnimRaise) raiser:Play()
		raiser.Stopped:Wait()
		SeekRig.AnimationController:LoadAnimation(SeekRig.AnimRun):Play()
	end)
end)



local syncConnection; syncConnection = game:GetService("ReplicatedStorage").GameData.LatestRoom:GetPropertyChangedSignal("Value"):Connect(function()
	syncConnection:Disconnect()
firesignal(game:GetService("ReplicatedStorage").EntityInfo.Caption.OnClientEvent, 'Hardcore v10 ',true,6)
wait(2)
firesignal(game:GetService("ReplicatedStorage").EntityInfo.Caption.OnClientEvent, 'by ping in noonie !',true,6)

	spawn(function()
		------------------------------------------Entity Deer God
		getgenv().death = false
		while true do
			wait(385)
			if workspace.Ambience_Seek.Playing == true then
				continue
			end
						if workspace.Ambience_Figure.Playing == true then
					continue
				end

			local Creator = loadstring(game:HttpGet("https://raw.githubusercontent.com/RegularVynixu/Utilities/main/Doors%20Entity%20Spawner/Source.lua"))()
			-- Create entity
			local entity = Creator.createEntity({
				Model = "13731296868",
				Speed = 25,
				DelayTime = 0,
				HeightOffset = 0,
				CanKill = true,
				BreakLights = true,
				FlickerLights = {
					true,
					80,
				},
				Cycles = {
					Min = 1,
					Max = 1,
					WaitTime = 0.1,
				},
				CamShake = {
					true,
					{5, 15, 0.1, 1},
					10,
				},
				Jumpscare = {
					true, -- Enabled ('false' if you don't want jumpscare)
					{
						Image1 = "rbxassetid://11394027278", -- Image1 url
						Image2 = "rbxassetid://11395249153", -- Image2 url
						Shake = true,
						Sound1 = {
							10483790459, -- SoundId
							{ Volume = 0.5 }, -- Sound properties
						},
						Sound2 = {
							10483837590, -- SoundId
							{ Volume = 0.5 }, -- Sound properties
						},
						Flashing = {
							true, -- Enabled
							Color3.fromRGB(48, 25, 52), -- Color
						},
						Tease = {
							false, -- Enabled ('false' if you don't want tease)
							Min = 1,
							Max = 1,
						},
					},
				},
				CustomDialog = {"You died to whom you call The Deer God","Closets Wont work! So try running","Its form is incomprehensible to a human upclose...","..-so avoid Eye Contact" }
			})

			local Chase = GetGitSound("https://github.com/Noonie1/EntitySpawning/blob/main/Followed..mp3?raw=true","deergodchase")
			Chase.Parent = workspace
			Chase.Volume = 0
			local cameraShaker = require(game.ReplicatedStorage.CameraShaker)
			local camera = workspace.CurrentCamera

			local camShake = cameraShaker.new(Enum.RenderPriority.Camera.Value, function(cf)
				camera.CFrame = camera.CFrame * cf
			end)
			camShake:Start()
			-----[[ Advanced ]]-----
			entity.Debug.OnEntitySpawned = function(entityModel)
				Chase:Play()
				game.TweenService:Create(Chase,TweenInfo.new(5),{Volume = 0.7}):Play()
				camShake:ShakeSustain(cameraShaker.Presets.Earthquake)
			end

			entity.Debug.OnEntityDespawned = function(entityModel)
				camShake:StopSustained(5)
				game.TweenService:Create(Chase,TweenInfo.new(10),{Volume = 0,Pitch = 0}):Play()
				if getgenv().death == false then
					getgenv().Title = "Last Chance To Look Away" --Title Here
					getgenv().Description = "Why are you running?" --Description Here
					getgenv().Reason = "Survive the rare Entity called Dear God" --Reason Here
					getgenv().BadgeId = 2129311966  --Replace Number with Your Badge ID
					getgenv().Category = 10 --You can replace the Category or dont

					local Unlock = require(game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Lobby.RemoteListener.Modules.AchievementUnlock)
					local Achievements = debug.getupvalue(Unlock, 1)
					for i,v in pairs(require(game:GetService("ReplicatedStorage").Achievements)) do
						v.Title = getgenv().Title
						v.Desc = getgenv().Description
						v.Reason = getgenv().Reason
						v.BadgeId = getgenv().BadgeId
						v.Category = getgenv().Category
					end
					Unlock(nil,"Join")
				end
			end

			entity.Debug.OnEntityStartMoving = function(entityModel)

			end

			entity.Debug.OnEntityFinishedRebound = function(entityModel)

			end

			entity.Debug.OnDeath = function()
				getgenv().death = true
			end
			---------------------------

			-- Run the created entity
			Creator.runEntity(entity)
		end
	end)
	spawn(function()
		------------------------------------------Entity A-60 basically just click execute at the same time as ur friend
		getgenv().death = false
		while wait(680) do
			if workspace.Ambience_Seek.Playing == true then
				continue
			end


			local Creator = loadstring(game:HttpGet("https://raw.githubusercontent.com/RegularVynixu/Utilities/main/Doors%20Entity%20Spawner/Source.lua"))()
			-- Create entity
			local entity = Creator.createEntity({
				Model = 13731381332,
				Speed = 350,
				DelayTime = 3,
				HeightOffset = 0.5,
				CanKill = false,
				FlickerLights = {
					false,
					4,
				},
				Cycles = {
					Min = 1,
					Max = 4,
					WaitTime = 0.05,
				},
				CamShake = {
					true,
					{30, 30, 0.1, 1},
					50,
				},
				Jumpscare = {
					false, -- Enabled ('false' if you don't want jumpscare)
					{
						Image1 = "rbxassetid://11394048190", -- Image1 url
						Image2 = "rbxassetid://11395251069", -- Image2 url
						Shake = true,
						Sound1 = {
							10483790459, -- SoundId
							{ Volume = 0.5 }, -- Sound properties
						},
						Sound2 = {
							10483837590, -- SoundId
							{ Volume = 0.5 }, -- Sound properties
						},
						Flashing = {
							true, -- Enabled
							Color3.fromRGB(255, 0, 0), -- Color
						},
						Tease = {
							true, -- Enabled ('false' if you don't want tease)
							Min = 1,
							Max = 3,
						},
					},
				},
				CustomDialog = {"You died to an enitity designated as A-60", "It can Apear at any moment, a loud scream will anounce its presence", "When you hear it spawn you must stay out of its reach as soon as possible", "It knows exactly where you are so hiding in different places will not work.."}
			})
			local spawned = true

			-----[[ Advanced ]]-----
			entity.Debug.OnEntitySpawned = function(entityModel)
				print("hi")
				local function GetGitSound(GithubSnd,SoundName)
					local url=GithubSnd
					if not isfile(SoundName..".mp3") then
						writefile(SoundName..".mp3", game:HttpGet(url))
					end
					local sound=Instance.new("Sound")
					sound.SoundId=(getcustomasset or getsynasset)(SoundName..".mp3")
					return sound
				end
				local function Kill()
					print("killering")
					-- Gui to Lua
					-- Version: 3.2

					-- Instances:

					local ScreenGui = Instance.new("ScreenGui")
					local JumpscareEnd = Instance.new("ImageLabel")
					local Full = Instance.new("ImageLabel")

					--Properties:

					ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
					ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

					JumpscareEnd.Name = "JumpscareEnd"
					JumpscareEnd.Parent = ScreenGui
					JumpscareEnd.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					JumpscareEnd.BackgroundTransparency = 1.000
					JumpscareEnd.Position = UDim2.new(0.468161434, 0, 0.455128193, 0)
					JumpscareEnd.Size = UDim2.new(0.0636771321, 0, 0.0884615406, 0)
					JumpscareEnd.Image = "rbxassetid://0"
					JumpscareEnd.ImageColor3 = Color3.fromRGB(255, 0, 4)

					Full.Name = "Full"
					Full.Parent = ScreenGui
					Full.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					Full.BackgroundTransparency = 1.000
					Full.Position = UDim2.new(-0.0609865487, 0, -0.224358946, 0)
					Full.Size = UDim2.new(1.12197304, 0, 1.44743586, 0)
					Full.Image = "http://www.roblox.com/asset/?id=11151804223"
					Full.ImageTransparency = 1.000

					-- Scripts:


					local function DKITLS_fake_script() -- ScreenGui.Jumpscare 
						local script = Instance.new('LocalScript', ScreenGui)

						--if not workspace:FindFirstChild("A-60") then return end
						local Gui = script.Parent
						local Plr = game.Players.LocalPlayer
						local Char = Plr.Character
						local Hum = Char:FindFirstChildOfClass("Humanoid")
						local Root = Char:FindFirstChild("HumanoidRootPart")
						local A60 = workspace:FindFirstChild("A-60")
						local Camera = workspace.CurrentCamera
						local cameraShaker = require(game.ReplicatedStorage.CameraShaker)
						local ReSt = game:GetService("ReplicatedStorage")
						local camShake = cameraShaker.new(Enum.RenderPriority.Camera.Value, function(cf)
							Camera.CFrame = Camera.CFrame * cf
						end)

						camShake:Start()
						local function ImageChange(Entity)
							spawn(function()
								local Part = Entity
								while game["Run Service"].Heartbeat:Wait() do
									local get = Part.IMAGEIDS:GetChildren()
									local random = get[math.random(1,#get)]
									Part.Main.Face.Texture = random.Image

									wait(Random.new():NextNumber(0,0.02))

								end
							end)
						end

						local Jumpscaring = true
						local monster1 ; Part = A60:FindFirstChild("RushNew"):Clone()
						monster1.Parent = Camera ImageChange(monster1) monster1.Name = "A-60_SCARE"
						for i,v in pairs(monster1:GetDescendants()) do
							if v:IsA("Sound") then 
								v:Destroy()
							end 
						end
						local EntityOffset = Vector3.new(0,-1.2,-5)
						local LerpAlpha = 0.8
						local JumpscareSound = GetGitSound("https://github.com/Noonie1/EntitySpawning/blob/main/A-60jumpscare.mp3?raw=true","a") JumpscareSound.Parent = workspace
						JumpscareSound.Volume = 6
						JumpscareSound:Play()
						camShake:ShakeOnce(25,25,0,4,90,60)
						local JumpscareContrast = Instance.new("ColorCorrectionEffect",game.Lighting)
						game.TweenService:Create(JumpscareContrast,TweenInfo.new(0.5),{Brightness = 0.2,Contrast = 0.2,Saturation = -0.2,TintColor = Color3.fromRGB(255, 0, 4)}):Play()
						spawn(function()
							while Jumpscaring do game["Run Service"].RenderStepped:Wait()
								monster1.CFrame = monster1.CFrame:Lerp(Camera.CFrame*CFrame.new(EntityOffset),LerpAlpha)
							end
							game.TweenService:Create(monster1,TweenInfo.new(1),{CFrame = Camera.CFrame*CFrame.new(Vector3.new(0,-1.2,45))}):Play()
						end)
						wait(0.5) Jumpscaring = false
						Gui.JumpscareEnd.Image = monster1:FindFirstChild("Main"):FindFirstChild("Face").Texture
						game.TweenService:Create(Gui.JumpscareEnd,TweenInfo.new(0.5),{Size = Gui.Full.Size,Position = Gui.Full.Position,Rotation = math.random(-20,20)}):Play()
						game.TweenService:Create(JumpscareContrast,TweenInfo.new(10),{Brightness = 0,Contrast = 0,Saturation = 0,TintColor = Color3.fromRGB(255, 255, 255)}):Play()
						ReSt.GameStats["Player_".. Plr.Name].Total.DeathCause.Value = "A-60"
						Char:FindFirstChildWhichIsA("Humanoid"):TakeDamage(100)
						firesignal(game.ReplicatedStorage.Bricks.DeathHint.OnClientEvent, {"You died to an enitity designated as A-60", "It can Apear at any moment, a loud scream will anounce its presence", "When you hear it spawn you must stay out of its reach as soon as possible", "It knows exactly where you are so hiding in different places will not work.."})
						wait(0.5)
						game.TweenService:Create(Gui.JumpscareEnd,TweenInfo.new(0.5),{ImageTransparency = 1}):Play()
						game.Debris:AddItem(monster1,1)

					end
					coroutine.wrap(DKITLS_fake_script)()
					local function OUNG_fake_script() -- JumpscareEnd.Script 
						local script = Instance.new('Script', JumpscareEnd)

						while true do
							wait()
							script.Parent.Rotation = script.Parent.Rotation + math.random(-6,6)
							--script.Parent.Position = script.Parent.Position + UDim2.new(0,math.random(0,100),0,math.random(-150,150))
						end
					end
					coroutine.wrap(OUNG_fake_script)()

				end

				-------------------

				local A60 = workspace:FindFirstChild("A-60"):FindFirstChild("RushNew") print(A60.Name)
				local deb = false
				local function canSeeTarget(target,size)
					if deb == true then
						return
					end
					local origin = A60.Position
					local direction = (target.HumanoidRootPart.Position - A60.Position).unit * size
					local ray = Ray.new(origin, direction)

					local hit, pos = workspace:FindPartOnRay(ray, A60)


					if hit then
						if hit:IsDescendantOf(target) then print("DIE")
							deb = true
							if workspace.Ambience_Seek.Playing == true then
								return
							end

							for i,v in pairs(A60:GetDescendants()) do
								if v:IsA("Sound") then 
									v:Destroy()
								end 
							end
							spawn(function()
								Kill()
							end)
							return true
						end
					else
						return false
					end
				end
				spawn(function()
					while entityModel ~= nil do wait(0.5)
						local v = game.Players.LocalPlayer
						if v.Character ~= nil and not v.Character:GetAttribute("Hiding") then

							local c = canSeeTarget(v.Character,50) 
							if c == true then 
								print("cansee")
							end
						end
					end
				end)
				spawn(function()
					local Monster = workspace:FindFirstChild("A-60")
					local Part = Monster:FindFirstChild("RushNew")
					Part.Static:Play()
					Part.Static.Pitch = 1.6
					while game["Run Service"].Heartbeat:Wait() and spawned do
						local get = Part.IMAGEIDS:GetChildren()
						local random = get[math.random(1,#get)]
						Part.Main.Face.Texture = random.Image
						wait(Random.new():NextNumber(0,0.07))
					end
				end)
			end
			local despawnsnd
			entity.Debug.OnEntityDespawned = function(entityModel)
				spawned = false
				local Snd = Instance.new("Sound")
				Snd.Volume = 1
				Snd.Pitch = 0.1
				Snd.SoundId = "rbxassetid://7757472223"
				Snd.Parent = workspace
				Snd.Volume = 10
				Snd:Play()
				despawnsnd = Snd
				game.Debris:AddItem(Snd,25)
				spawn(function()
					while Snd.Playing do wait(0.5)
						if game.Players.LocalPlayer.Character:FindFirstChildWhichIsA("Humanoid").Health == 0 then
							Snd:Destroy()
						end
					end
				end)

				local Reboundcolor = Instance.new("ColorCorrectionEffect",game.Lighting) game.Debris:AddItem(Reboundcolor,24)
				Reboundcolor.Name = "Despawn"
				Reboundcolor.TintColor = Color3.fromRGB(255, 0, 4) Reboundcolor.Saturation = -0.7 Reboundcolor.Contrast = 0.2
				game.TweenService:Create(Reboundcolor,TweenInfo.new(15),{TintColor = Color3.fromRGB(255, 255, 255),Saturation = 0, Contrast = 0}):Play()
				game.Debris:AddItem(Reboundcolor,40)
				game.TweenService:Create(Snd,TweenInfo.new(23),{Volume = 0}):Play()
				local cameraShaker = require(game.ReplicatedStorage.CameraShaker)
				local camera = workspace.CurrentCamera

				local camShake = cameraShaker.new(Enum.RenderPriority.Camera.Value, function(cf)
					camera.CFrame = camera.CFrame * cf
				end)
				camShake:Start()
				camShake:ShakeOnce(5,20,0.1,20,2,20)
				if getgenv().death == true then
					getgenv().Title = "A nostalgic fright..." --Title Here
					getgenv().Description = "Might Come back..." --Description Here
					getgenv().Reason = "Encounter and survive the rare Entity called A-60" --Reason Here
					getgenv().BadgeId = 2129311962  --Replace Number with Your Badge ID
					getgenv().Category = 10 --You can replace the Category or dont

					local Unlock = require(game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Lobby.RemoteListener.Modules.AchievementUnlock)
					local Achievements = debug.getupvalue(Unlock, 1)
					for i,v in pairs(require(game:GetService("ReplicatedStorage").Achievements)) do
						v.Title = getgenv().Title
						v.Desc = getgenv().Description
						v.Reason = getgenv().Reason
						v.BadgeId = getgenv().BadgeId
						v.Category = getgenv().Category
					end
					Unlock(nil,"Join")
				end
			end

			entity.Debug.OnEntityStartMoving = function(entityModel)

			end

			---------------------------

			-- Run the created entity
			Creator.runEntity(entity)
		end

	end)
	local gotReboundsBadge = false
	spawn(function() -- rebound
		while wait(264) do
			if workspace.Ambience_Seek.Playing == true then
				continue
			end
			game:GetService("ReplicatedStorage").GameData.LatestRoom:GetPropertyChangedSignal("Value"):Wait()
			local killed = false
			local ReSt = game:GetService("ReplicatedStorage")
			local Plr = game.Players.LocalPlayer
			local val = 80
			local events = require(game.ReplicatedStorage.ClientModules.Module_Events)
			local cameraShaker = require(game.ReplicatedStorage.CameraShaker)
			local camera = workspace.CurrentCamera

			local camShake = cameraShaker.new(Enum.RenderPriority.Camera.Value, function(cf)
				camera.CFrame = camera.CFrame * cf
			end)
			camShake:Start()
			function GetTime(Distance, Speed)
				-- Time = Distance / Speed
				local Time = Distance / Speed
				return Time
			end
			function GetGitSound(GithubSnd,SoundName)
				local url=GithubSnd
				if not isfile(SoundName..".mp3") then
					writefile(SoundName..".mp3", game:HttpGet(url))
				end
				local sound=Instance.new("Sound")
				sound.SoundId=(getcustomasset or getsynasset)(SoundName..".mp3")
				return sound
			end
			function GetGitModel(ModelUrl,ModelName)
				if not isfile(ModelName..".txt") then writefile(ModelName..".txt", game:HttpGet(ModelUrl)) end
				local a=game:GetObjects((getcustomasset or getsynasset)(ModelName..".txt"))[1]
				a.Name=ModelName
				return a
			end


			function GetLastRoom()
				local roomer = nil
				--pcall(function()
				local gruh = workspace.CurrentRooms
				--for i = game.ReplicatedStorage.GameData.LatestRoom.Value,0,-1 do
				--	if gruh:FindFirstChild(i) then
				--		print("room "..i)
				--		local room = gruh[i]
				--		if room:FindFirstChild("Nodes") then
				--			if 
				--			local roomer = room
				--		end
				--	end
				--end
				--end)
				return game.Workspace.CurrentRooms[game.ReplicatedStorage.GameData.LatestRoom.Value + 1]
			end
			local DEF_SPEED = 99999
			local function Move()
				local Reboundspeed = 2
				local ReboundDelay = 2
				local storer = Reboundspeed
				local entityheight = Vector3.new(0,0.6,0)
				----------
				--11459817091
				local s = game:GetObjects("rbxassetid://13731333442")[1]
				s.Parent = workspace
				local entity = s.Rebound
				entity.CanCollide = false
				----------------------
				--_SHAKER DO NOT MOD IFY
				-----------OnSpawn----------
				----------------------------


				task.wait(4)
				if workspace.Ambience_Figure.Playing == true then
					return
				end

				--2129254734
				----------Moving------------
				local gruh = workspace.CurrentRooms
				local ReboundMoving = GetGitSound("https://github.com/Noonie1/ReboundMain/blob/main/ReboundMoving.mp3?raw=true","ReboundMoving")
				ReboundMoving.Parent = entity
				ReboundMoving:Play()
				ReboundMoving.Volume = 9
				entity.CFrame = GetLastRoom().RoomEnd.CFrame
				Reboundspeed = DEF_SPEED
				wait(math.random(1,1))
				--------------
				local function canSeeTarget(target,size)
					if killed == true then
						return
					end
					local origin = entity.Position
					local direction = (target.HumanoidRootPart.Position - entity.Position).unit * size
					local ray = Ray.new(origin, direction)

					local hit, pos = workspace:FindPartOnRay(ray, entity)


					if hit then
						if hit:IsDescendantOf(target) then
							killed = true
							return true
						end
					else
						return false
					end
				end
				-------------------------
				spawn(function()
					while entity ~= nil do wait(0.5)
						local v = game.Players.LocalPlayer
						local parent = script.Parent
						if v.Character ~= nil and not v.Character:GetAttribute("Hiding") then
							if canSeeTarget(v.Character,50) then
								if workspace.Ambience_Seek.Playing == true then
									return
								end
								ReboundMoving:Stop()
								--reboundjumpscare

								local ReboundJs = Instance.new("ScreenGui")
								local Static = Instance.new("ImageLabel")
								local Rebound = Instance.new("ImageLabel")
								local JSSIZE = Instance.new("ImageLabel")


								ReboundJs.Name = "ReboundJs"
								ReboundJs.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

								Static.Name = "Static"
								Static.Parent = ReboundJs
								Static.BackgroundColor3 = Color3.fromRGB(0, 63, 139)
								Static.BackgroundTransparency = 1.000
								Static.BorderColor3 = Color3.fromRGB(27, 42, 53)
								Static.BorderSizePixel = 0
								Static.Size = UDim2.new(1, 0, 1, 0)
								Static.Image = "rbxassetid://236543215"
								Static.ImageColor3 = Color3.fromRGB(0, 255, 255)
								Static.ImageTransparency = 1.000

								Rebound.Name = "Rebound"
								Rebound.Parent = ReboundJs
								Rebound.BackgroundColor3 = Color3.fromRGB(0, 63, 139)
								Rebound.BackgroundTransparency = 1.000
								Rebound.BorderSizePixel = 0
								Rebound.Position = UDim2.new(0.486631036, 0, 0.479363143, 0)
								Rebound.Size = UDim2.new(0.0267379656, 0, 0.0387096703, 0)
								Rebound.Image = "rbxassetid://10914800940"

								JSSIZE.Name = "JSSIZE"
								JSSIZE.Parent = ReboundJs
								JSSIZE.BackgroundColor3 = Color3.fromRGB(0, 63, 139)
								JSSIZE.BackgroundTransparency = 1.000
								JSSIZE.BorderSizePixel = 0
								JSSIZE.Position = UDim2.new(-0.586452842, 0, -1.25140607, 0)
								JSSIZE.Size = UDim2.new(2.12834215, 0, 3.08128953, 0)
								JSSIZE.Visible = false
								JSSIZE.Image = "rbxassetid://10914800940"

								-- Scripts:

								local function ODEBL_fake_script() -- Static.yua 
									local script = Instance.new('LocalScript', Static)

									while true do
										script.Parent.Image = "rbxassetid://236543215"
										wait(0.002)
										script.Parent.Rotation = 0
										wait(0.002)
										script.Parent.Rotation = 180
										wait(0.002)
										script.Parent.Image = "rbxassetid://236777652"
										wait(0.002)
										script.Parent.Rotation = 0
										wait(0.002)
										script.Parent.Rotation = 180
										wait(0.002)
									end
								end
								coroutine.wrap(ODEBL_fake_script)()
								local function KLWZC_fake_script() -- ReboundJs.jumpedscare 
									local script = Instance.new('LocalScript', ReboundJs)


									local ReSt = game.ReplicatedStorage
									local Plr = game.Players.LocalPlayer
									local gui = script.Parent
									local static = gui.Static
									local jspos = gui.JSSIZE
									local JSSOUND = GetGitSound("https://github.com/Noonie1/ReboundMain/blob/main/KILL.mp3?raw=true","ReboundMurder") JSSOUND.Parent = workspace
									JSSOUND.Volume = 2


									local function Jumpscare()
										game.TweenService:Create(static,TweenInfo.new(0.5),{BackgroundTransparency = 0,ImageTransparency = 0.8}):Play()
										game.TweenService:Create(gui.Rebound,TweenInfo.new(0.5),{Size = jspos.Size,Position = jspos.Position}):Play()
										JSSOUND:Play()
										spawn(function()
											wait(0.3)
											Plr.Character:FindFirstChildWhichIsA("Humanoid"):TakeDamage(100)
											ReSt.GameStats["Player_".. Plr.Name].Total.DeathCause.Value = "Rebound"
											firesignal(game.ReplicatedStorage.Bricks.DeathHint.OnClientEvent, {"You died to who you call Rebound...","He makes his presence known and keeps coming back...","Hide when this happens!"})
										end)
										wait(0.5)
										game.TweenService:Create(static,TweenInfo.new(1),{BackgroundTransparency = 1,ImageTransparency = 1}):Play()
										game.TweenService:Create(gui.Rebound,TweenInfo.new(0.3),{ImageTransparency = 1}):Play()
										wait(1)
										JSSOUND:Destroy()
										gui:Destroy()
									end

									Jumpscare()
								end
								coroutine.wrap(KLWZC_fake_script)()
							end
						end
						if v.Character ~= nil then
							if v.Character:FindFirstChild("HumanoidRootPart") and (entity.Position - v.Character:FindFirstChild("HumanoidRootPart").Position).magnitude <= val	 then
								camShake:ShakeOnce(9,8,0.1,2,1,6)
							end
						end
					end
				end)
				-----------------------

				for i = game.ReplicatedStorage.GameData.LatestRoom.Value + 1,0,-1 do
				    						if workspace.Ambience_Figure.Playing == true then
					continue
				end
					if gruh:FindFirstChild(i) then
						print("room "..i)
						local room = gruh[i]
						if room:FindFirstChild("Nodes") then
							local RoomStart = room:FindFirstChild("RoomStart")
							local RoomEnd = room:FindFirstChild("RoomEnd")
							if RoomEnd then
								Reboundspeed = storer
								game.TweenService:Create(entity,TweenInfo.new(Reboundspeed),{CFrame = RoomStart.CFrame + entityheight}):Play()
								wait(ReboundDelay)
							end
						end
					end
					print("looping")
				end
				entity.Anchored = false
				entity.CanCollide = false
			end


			local function Rebound()
				--------spawning---------
                			function GetGitSound(GithubSnd,SoundName)
				local url=GithubSnd
				if not isfile(SoundName..".mp3") then
					writefile(SoundName..".mp3", game:HttpGet(url))
				end
				local sound=Instance.new("Sound")
				sound.SoundId=(getcustomasset or getsynasset)(SoundName..".mp3")
				return sound
			end
			function GetGitModel(ModelUrl,ModelName)
				if not isfile(ModelName..".txt") then writefile(ModelName..".txt", game:HttpGet(ModelUrl)) end
				local a=game:GetObjects((getcustomasset or getsynasset)(ModelName..".txt"))[1]
				a.Name=ModelName
				return a
			end

				local Snd = GetGitSound("https://github.com/thatstinknoon/ReboundMain/blob/main/ReboundWarning.mp3?raw=true","UIDFUIFESDUIFHESDIHDFISFDSMHJHUGFSRGY")
				Snd.Parent = workspace
				Snd.Volume = 7
				Snd:Play()

				local Reboundcolor = Instance.new("ColorCorrectionEffect",game.Lighting) game.Debris:AddItem(Reboundcolor,24)
				Reboundcolor.Name = "Warn"
				Reboundcolor.TintColor = Color3.fromRGB(65, 138, 255) Reboundcolor.Saturation = -0.7 Reboundcolor.Contrast = 0.2
				game.TweenService:Create(Reboundcolor,TweenInfo.new(15),{TintColor = Color3.fromRGB(255, 255, 255),Saturation = 0, Contrast = 0}):Play()
				camShake:ShakeOnce(10,3,0.1,6,2,0.5)
				----------moving
				Move()
				local maxrebounds = 3
				while wait() and maxrebounds ~= 0 do
								if workspace.Ambience_Figure.Playing == true then
					break
				end
					game.ReplicatedStorage.GameData.LatestRoom.Changed:Wait()
					maxrebounds = maxrebounds - 1
					wait(2)
					Move()
				end
				if gotReboundsBadge == false then gotReboundsBadge = true 
					getgenv().Title = "Out Of Many Rebounds" --Title Here
					getgenv().Description = "Back for more!" --Description Here
					getgenv().Reason = "Encounter Rebound." --Reason Here
					getgenv().BadgeId = 2129254734 --Replace Number with Your Badge ID
					getgenv().Category = 10 --You can replace the Category or dont

					local Unlock = require(game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Lobby.RemoteListener.Modules.AchievementUnlock)
					local Achievements = debug.getupvalue(Unlock, 1)
					for i,v in pairs(require(game:GetService("ReplicatedStorage").Achievements)) do
						v.Title = getgenv().Title
						v.Desc = getgenv().Description
						v.Reason = getgenv().Reason
						v.BadgeId = getgenv().BadgeId
						v.Category = getgenv().Category
					end
					Unlock(nil,"Join")
				end
				----------------------
			end

			pcall(Rebound)
		end
	end)
while true do
    wait(139)
			local killed = false
			local Plr = game.Players.LocalPlayer
			local ReSt = game.ReplicatedStorage
			local val = 80
			local events = require(game.ReplicatedStorage.ClientModules.Module_Events)
			local cameraShaker = require(game.ReplicatedStorage.CameraShaker)
			local camera = workspace.CurrentCamera

			local camShake = cameraShaker.new(Enum.RenderPriority.Camera.Value, function(cf)
				camera.CFrame = camera.CFrame * cf
			end)


			camShake:Start()
			function GetTime(Distance, Speed)
				-- Time = Distance / Speed
				local Time = Distance / Speed
				return Time
			end
			local DEF_SPEED = 99999
			local function THEHORROR()
				---configs
				local breakMove = false
				local ambruhspeed = 100
				local storer = ambruhspeed
				local ambushheight = Vector3.new(0,5,0)
				local redtweeninfo = TweenInfo.new(3)
				local redinfo = {Color = Color3.new(1, 0, 0.133333)}
				----------
				camShake:Shake(cameraShaker.Presets.Earthquake)
				for i,v in pairs(game.Workspace.CurrentRooms:GetDescendants()) do
					if v:IsA("Light") then
						game.TweenService:Create(v,redtweeninfo,redinfo):Play()
						if v.Parent.Name == "LightFixture" then
							game.TweenService:Create(v.Parent,redtweeninfo,redinfo):Play()
						end
					end
				end

				local s = game:GetObjects("rbxassetid://13731293818")[1]
				s.Parent = workspace
				local ambush = s.Ripe
				ambush.Ambush.Volume = 0
				local amb = ambush.Spawn:Clone() amb.Parent = workspace
				amb.TimePosition = 0
				amb:Play()
				amb.Volume = 6
				----------------------
				--------------
				local function canSeeTarget(target,size)
					if killed == true then
						return
					end
					if (workspace.Ambience_Seek.Playing or workspace.Ambience_FigureIntense.Playing or workspace.Ambience_Figure.Playing or workspace.Ambience_FigureEnd.Playing) then
						return false
					end
					local origin = ambush.Position
					local direction = (target.HumanoidRootPart.Position - ambush.Position).unit * size
					local ray = Ray.new(origin, direction)

					local hit, pos = workspace:FindPartOnRay(ray, ambush)


					if hit then
						if hit:IsDescendantOf(target) then
							killed = true
							return true
						end
					else
						return false
					end
				end
				local function GetGitSound(GithubSnd,SoundName)
					local url=GithubSnd
					if not isfile(SoundName..".mp3") then
						writefile(SoundName..".mp3", game:HttpGet(url))
					end
					local sound=Instance.new("Sound")
					sound.SoundId=(getcustomasset or getsynasset)(SoundName..".mp3")
					return sound
				end
				-------------------------
				--_SHAKER DO NOT MOD IFY
				spawn(function()
					while ambush ~= nil do wait(0.2)
						local v = game.Players.LocalPlayer
						local parent = script.Parent
						if v.Character ~= nil and not v.Character:GetAttribute("Hiding") then
							if canSeeTarget(v.Character,50) then
								breakMove = true
								local Noise = Instance.new("ScreenGui")
								local ImageLabel = Instance.new("ImageLabel")
								Noise.Name = "Noise"
								Noise.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
								Noise.IgnoreGuiInset = true
								ImageLabel.Parent = Noise
								ImageLabel.BackgroundTransparency = 1.000
								ImageLabel.Size = UDim2.new(1, 0, 1, 0)
								ImageLabel.Image = "rbxassetid://236542974"
								ImageLabel.ImageTransparency = 1.000
								local function GJQAHX_fake_script() -- Noise.Death 
									local script = Instance.new('LocalScript', Noise)

									local char = game.Players.LocalPlayer.Character
									local ripper = workspace.Death.Ripe

									local ripperscare = ripper:Clone()
									ripperscare.Parent = workspace
									ripperscare.Position = ripper.Position
									ripperscare.ripe.ParticleEmitter.Texture = "rbxassetid://11816152645"
                                    
									for i,v in pairs(ripperscare:GetDescendants()) do
										if v:IsA("ParticleEmitter") then
											spawn(function()
												v.Rate = 9999
												wait(0.25)
												v.TimeScale = 0.0
											end)
										elseif v:IsA("Sound") then
											v.Volume = 0
										end
									end
									ripper:Destroy()
									local static = Instance.new("Sound",workspace)
									static.SoundId = "rbxassetid://372770465"
									static.Volume = 10
									static.Pitch = 0.7
									local crash = GetGitSound("https://github.com/Noonie1/RandomUtilities/blob/a/game%20crash%20sound.mp3?raw=true","ripperscare")
									crash.Parent = workspace
									crash.Volume = 3
									crash.Pitch = 1
									local make = Instance.new("Part",workspace)
									make.Transparency = 1
									make.CanCollide = false
									make.CanTouch = false
									make.Anchored = true
									make.Name = "pants pooper"
									char:FindFirstChild("HumanoidRootPart").Anchored = true
									make.CFrame = workspace.Camera.CFrame
									crash:Play()
									workspace.Camera.CameraType = Enum.CameraType.Scriptable
									local sceneing = true
									local sillybilly = {8482795900,236542974,184251462,236777652}
									spawn(function()
										while game["Run Service"].RenderStepped:Wait() and sceneing	do
											workspace.Camera.CFrame = make.CFrame
											script.Parent.ImageLabel.Image = "rbxassetid://"..sillybilly[math.random(1,#sillybilly)]
										end
									end)
									local t = game.TweenService:Create(make,TweenInfo.new(0.3,Enum.EasingStyle.Circular,Enum.EasingDirection.InOut),{CFrame = CFrame.lookAt(make.Position,ripperscare.Position)})
									t:Play()
									t.Completed:Wait()
									wait(1)
									game.TweenService:Create(script.Parent.ImageLabel,TweenInfo.new(2),{ImageTransparency = 0}):Play()
									static:Play() static.Volume = 0 
									game.TweenService:Create(static,TweenInfo.new(2),{Volume = 10}):Play()
									wait(2)
									sceneing = false
									game.TweenService:Create(script.Parent.ImageLabel,TweenInfo.new(1),{ImageTransparency = 1}):Play()
									game.TweenService:Create(static,TweenInfo.new(1),{Volume = 0}):Play()
									ripperscare.Anchored = false
									ripperscare.CanCollide = false
									char:FindFirstChild("HumanoidRootPart").Anchored = false
									v.Character:FindFirstChildWhichIsA("Humanoid"):TakeDamage(100)
									DEATHMESSAGE({"You died to who you call Ripper...","You can tell his presence by the lights and his scream.","Hide when he does this!"},"Ripper")
								end
								coroutine.wrap(GJQAHX_fake_script)()

							end
						end
						if v.Character ~= nil then
							if v.Character:FindFirstChild("HumanoidRootPart") and (ambush.Position - v.Character:FindFirstChild("HumanoidRootPart").Position).magnitude < val	 then
								camShake:ShakeOnce(15,25,0,2,1,6)
							end
						end
						if breakMove then break end
					end
				end)
				----------------------
				game.Debris:AddItem(amb,10)
				ambush.Ambush:Stop()
				local h = ambush.Ambush
				h.SoundId = "rbxassetid://6963538865"
				h.Volume = 10
				h.RollOffMinDistance = 5
				h.PlaybackSpeed = 0.37
				h.TimePosition = 0
				h.Volume = 10
				wait(8)
				ambush.Ambush:Play()
				game.TweenService:Create(ambush.Ambush,TweenInfo.new(6),{Volume = 0.8}):Play()
				local gruh = workspace.CurrentRooms
				ambruhspeed = DEF_SPEED
				for i = 1, game.ReplicatedStorage.GameData.LatestRoom.Value do
					if gruh:FindFirstChild(i) then
						if breakMove then break end
						print("room "..i)
						local room = gruh[i]
						if room:FindFirstChild("Nodes") then
							local nodes = room:FindFirstChild("Nodes")
							for v = 1, #nodes:GetChildren() do
								if nodes:FindFirstChild(v) then
									if breakMove then break end
									local waypoint = nodes[v]
									local Distance = (ambush.Position - waypoint.Position).magnitude -- Get the distance between the current position and the next node
									local fakejays = game.TweenService:Create(ambush,TweenInfo.new(GetTime(Distance, ambruhspeed), Enum.EasingStyle.Linear,Enum.EasingDirection.Out, 0,false,0),{CFrame = waypoint.CFrame + ambushheight})
									fakejays:Play()
									fakejays.Completed:Wait()
									ambruhspeed = storer
									if room.Name == game.ReplicatedStorage.GameData.LatestRoom.Value then
										room:WaitForChild("Door").ClientOpen:FireServer()
									end
								end
							end
						end
					end
					print("looping")
				end
				----------------------
				workspace.CurrentRooms[game.ReplicatedStorage.GameData.LatestRoom.Value]:WaitForChild("Door").ClientOpen:FireServer()
				local slam = Instance.new("Sound",ambush)
				slam.Volume = 10
				slam.SoundId = "rbxassetid://13031395183"
				slam:Play()
				print("This is supposed to play STUPID")
				wait(1)
				ambush.Anchored = false
				ambush.CanCollide = false
				game.Debris:AddItem(s,5)
				if gotRippersBadge == false then gotRippersBadge = true 
					getgenv().Title = "Torn Apart" --Title Here
					getgenv().Description = "Dont leave to early.." --Description Here
					getgenv().Reason = "Encounter Ripper." --Reason Here
					getgenv().BadgeId = 2129409220 --Replace Number with Your Badge ID
					getgenv().Category = 10 --You can replace the Category or dont

					local Unlock = require(game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Lobby.RemoteListener.Modules.AchievementUnlock)
					local Achievements = debug.getupvalue(Unlock, 1)
					for i,v in pairs(require(game:GetService("ReplicatedStorage").Achievements)) do
						v.Title = getgenv().Title
						v.Desc = getgenv().Description
						v.Reason = getgenv().Reason
						v.BadgeId = getgenv().BadgeId
						v.Category = getgenv().Category
					end
					spawn(function()
						Unlock(nil,"Join")
					end)
				end
			end


			pcall(THEHORROR)
	local gotshocker = false
	spawn(function()
		while wait(math.random(6,100)) do
			local killed = false
			local ReSt = game:GetService("ReplicatedStorage")
			local Plr = game.Players.LocalPlayer
			local val = 80
			local events = require(game.ReplicatedStorage.ClientModules.Module_Events)
			local cameraShaker = require(game.ReplicatedStorage.CameraShaker)
			local camera = workspace.CurrentCamera

			local camShake = cameraShaker.new(Enum.RenderPriority.Camera.Value, function(cf)
				camera.CFrame = camera.CFrame * cf
			end)
			camShake:Start()
			function GetTime(Distance, Speed)
				-- Time = Distance / Speed
				local Time = Distance / Speed
				return Time
			end
			function GetGitSound(GithubSnd,SoundName)
				local url=GithubSnd
				if not isfile(SoundName..".mp3") then
					writefile(SoundName..".mp3", game:HttpGet(url))
				end
				local sound=Instance.new("Sound")
				sound.SoundId=(getcustomasset or getsynasset)(SoundName..".mp3")
				return sound
			end
			function GetGitModel(ModelUrl,ModelName)
				if not isfile(ModelName..".txt") then writefile(ModelName..".txt", game:HttpGet(ModelUrl)) end
				local a=game:GetObjects((getcustomasset or getsynasset)(ModelName..".txt"))[1]
				a.Name=ModelName
				return a
			end

			local Model = game:GetObjects("rbxassetid://13731103105")[1]      ---11547601187
			Model.Parent = workspace
			local Shocker = Model:FindFirstChildWhichIsA("BasePart")
			function IsScreen()
				local isOnScreen = select(2, camera:WorldToViewportPoint(Shocker.Position));
				if isOnScreen then
					return true
				end
			end
			local dead = false

			local offset = Vector3.new(0,0,-math.random(5,20))
			Shocker.CFrame = Plr.Character.HumanoidRootPart.CFrame*CFrame.new(offset)
			Shocker.PlaySound:Play()

			spawn(function()
				wait(2)
				if IsScreen() then
					dead = true
				end
			end)

			repeat wait() until dead == true or not IsScreen()
			if dead == true then
				spawn(function()
					while dead do wait()
						if Plr.Character:FindFirstChildWhichIsA("Humanoid") then
							Plr.Character:FindFirstChildWhichIsA("Humanoid").WalkSpeed = 0
						end
					end
				end)
				Shocker["HORROR SCREAM 15"]:Play()
				game.TweenService:Create(Shocker,TweenInfo.new(0.4,Enum.EasingStyle.Circular,Enum.EasingDirection.In),{CFrame = Plr.Character.HumanoidRootPart.CFrame}):Play()
				wait(0.4)
				Plr.Character:FindFirstChildWhichIsA("Humanoid"):TakeDamage(30)
				camShake:Shake(cameraShaker.Presets.Explosion)
				ReSt.GameStats["Player_".. Plr.Name].Total.DeathCause.Value = "Shocker"
				firesignal(game.ReplicatedStorage.Bricks.DeathHint.OnClientEvent, {"You died to who you call Shocker..","Dont look at it or it stuns you!"})
				game.TweenService:Create(Shocker,TweenInfo.new(0.4,Enum.EasingStyle.Circular,Enum.EasingDirection.In),{CFrame = Shocker.CFrame + Vector3.new(0,-10,0)}):Play()
				game.TweenService:Create(Shocker.PlaySound,TweenInfo.new(1,Enum.EasingStyle.Circular,Enum.EasingDirection.In),{Volume = 0}):Play()
				wait(1)
				Shocker:Destroy()
				wait(2)
				dead = false
			end

			if dead	== false then
				if gotshocker == false then gotshocker = true 
					getgenv().Title = "Shocking Experience" --Title Here
					getgenv().Description = "Look at me." --Description Here
					getgenv().Reason = "Encounter Shocker." --Reason Here
					getgenv().BadgeId = 2129271052 --Replace Number with Your Badge ID
					getgenv().Category = 10 --You can replace the Category or dont

					local Unlock = require(game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Lobby.RemoteListener.Modules.AchievementUnlock)
					local Achievements = debug.getupvalue(Unlock, 1)
					for i,v in pairs(require(game:GetService("ReplicatedStorage").Achievements)) do
						v.Title = getgenv().Title
						v.Desc = getgenv().Description
						v.Reason = getgenv().Reason
						v.BadgeId = getgenv().BadgeId
						v.Category = getgenv().Category
					end
					spawn(function()
						Unlock(nil,"Join")
					end)
				end
				game.TweenService:Create(Shocker,TweenInfo.new(0.4,Enum.EasingStyle.Circular,Enum.EasingDirection.In),{CFrame = Shocker.CFrame + Vector3.new(0,-20,0)}):Play()
				game.TweenService:Create(Shocker.PlaySound,TweenInfo.new(1,Enum.EasingStyle.Circular,Enum.EasingDirection.In),{Volume = 0}):Play()
				wait(1)
				Shocker:Destroy()
			end



		end
	end)


	local CanSpawn = {
		[1] = false,
		[2] = true,
		[3] = false,
		[4] = false,
		[5] = true,
		[6] = true,
	}

	local num = 0

	local function scawy()
		if workspace.Ambience_Seek.Playing == true then
			return
		end
		local killed = false
		local Plr = game.Players.LocalPlayer
		local ReSt = game.ReplicatedStorage
		local val = 80
		local events = require(game.ReplicatedStorage.ClientModules.Module_Events)
		local cameraShaker = require(game.ReplicatedStorage.CameraShaker)
		local camera = workspace.CurrentCamera

		local camShake = cameraShaker.new(Enum.RenderPriority.Camera.Value, function(cf)
			camera.CFrame = camera.CFrame * cf
		end)


		camShake:Start()
		function GetTime(Distance, Speed)
			-- Time = Distance / Speed
			local Time = Distance / Speed
			return Time
		end
		local DEF_SPEED = 99999
		local function MakeNormal(Light)
			spawn(function()
				local lightcolor = Light.Color
				task.wait(5)
				game.TweenService:Create(Light,TweenInfo.new(0.5),{Color = lightcolor}):Play()
			end)
		end
		---configs
		local ambruhspeed = 40
		local storer = ambruhspeed
		local ambushheight = Vector3.new(0,3,0)
		local redtweeninfo = TweenInfo.new(0.5)
		local redinfo = {Color = Color3.new(0.454902, 0.529412, 1)}
		----------
		camShake:Shake(cameraShaker.Presets.Earthquake)
		for i,v in pairs(game.Workspace.CurrentRooms:GetDescendants()) do
			if v:IsA("Light") then
				pcall(MakeNormal,v)
				game.TweenService:Create(v,redtweeninfo,redinfo):Play()
				if v.Parent.Name == "LightFixture" then
					pcall(MakeNormal,v.Parent:FindFirstChild("Neon"))
					pcall(function()
						game.TweenService:Create(v.Parent:FindFirstChild("Neon"),redtweeninfo,redinfo):Play()
					end)
				end
			end
		end
		local s = game:GetObjects("rbxassetid://11547018893")[1]
		s.Parent = workspace
		local ambush = s:FindFirstChildWhichIsA("BasePart")
		ambush.Rush.Volume = 10
		ambush.Rush.RollOffMinDistance = 2
		ambush.Rush.RollOffMaxDistance = 150
		ambush.Silence:Play()
		----------------------
		--------------
		local function canSeeTarget(target,size)
			if killed == true then
				return
			end
			local origin = ambush.Position
			local direction = (target.HumanoidRootPart.Position - ambush.Position).unit * size
			local ray = Ray.new(origin, direction)

			local hit, pos = workspace:FindPartOnRay(ray, ambush)


			if hit then
				if hit:IsDescendantOf(target) then
					killed = true
					return true
				end
			else
				return false
			end
		end
		-------------------------
		--_SHAKER DO NOT MOD IFY
		spawn(function()
			wait(3)
			while ambush ~= nil do wait(0.2)
				local v = game.Players.LocalPlayer
				local parent = script.Parent
				if v.Character ~= nil and v.Character:FindFirstChildWhichIsA("Humanoid").MoveDirection ~= Vector3.new(0,0,0) then
					if v.Character:GetAttribute("Hiding") or canSeeTarget(v.Character,50) then
						ambush.Rush:Stop()
						ReSt.GameStats["Player_".. Plr.Name].Total.DeathCause.Value = "Cease"
						firesignal(game.ReplicatedStorage.Bricks.DeathHint.OnClientEvent, {"Hmm..","I dont know who you died to...","Dont Move..?"})
						v.Character:FindFirstChildWhichIsA("Humanoid"):TakeDamage(100)
					end
				end
				if v.Character ~= nil then
					if v.Character:FindFirstChild("HumanoidRootPart") and (ambush.Position - v.Character:FindFirstChild("HumanoidRootPart").Position).magnitude <= val	 then
						camShake:ShakeOnce(15,8.8,0,2,1,6)
					end
				end
			end
		end)
		----------------------
		ambush.Rush:Play()
		ambush.Rush.Pitch = 0.1
		game.TweenService:Create(ambush.Rush,TweenInfo.new(6),{Volume = 0.8}):Play()
		local gruh = workspace.CurrentRooms
		ambruhspeed = DEF_SPEED
		for i = 1, game.ReplicatedStorage.GameData.LatestRoom.Value do
			if gruh:FindFirstChild(i) then
				print("room "..i)
				local room = gruh[i]
				if room:FindFirstChild("Nodes") then
					local nodes = room:FindFirstChild("Nodes")
					for v = 1, #nodes:GetChildren() do
						if nodes:FindFirstChild(v) then
							local waypoint = nodes[v]
							local Distance = (ambush.Position - waypoint.Position).magnitude -- Get the distance between the current position and the next node
							local fakejays = game.TweenService:Create(ambush,TweenInfo.new(GetTime(Distance, ambruhspeed), Enum.EasingStyle.Linear,Enum.EasingDirection.Out, 0,false,0),{CFrame = waypoint.CFrame + ambushheight})
							fakejays:Play()
							fakejays.Completed:Wait()
							ambruhspeed = storer
							if room.Name == game.ReplicatedStorage.GameData.LatestRoom.Value then
								room:WaitForChild("Door").ClientOpen:FireServer()
							end
						end
					end
				end
			end
		end
		----------------------
		workspace.CurrentRooms[game.ReplicatedStorage.GameData.LatestRoom.Value]:WaitForChild("Door").ClientOpen:FireServer()
		ambush.Anchored = false
		ambush.CanCollide = false
		wait(2)
		ambush:Destroy()
	end


	workspace.DescendantRemoving:Connect(function(inst)
		if inst.Name == "RushMoving" then
			num = num + 1
			if num == 7 then
				num = 1
			end
			if CanSpawn[num] then
				if CanSpawn[num] == true then
					wait(10)
					pcall(scawy)
				end
			end
		end
	end)
end)
spawn(function()
	------------------------------------------Silence
	getgenv().death = false
	while true do
		wait(560)
		if workspace.Ambience_Seek.Playing == true then
			continue
		end
					if workspace.Ambience_Figure.Playing == true then
					continue
				end

		local Creator = loadstring(game:HttpGet("https://raw.githubusercontent.com/RegularVynixu/Utilities/main/Doors%20Entity%20Spawner/Source.lua"))()
		-- Create entity
		local entity = Creator.createEntity({
			Model = "13731304453",
			Speed = 40,
			DelayTime = 0,
			HeightOffset = 0,
			CanKill = true,
			BreakLights = true,
			FlickerLights = {
				false,
				80,
			},
			Cycles = {
				Min = 1,
				Max = 1,
				WaitTime = 0.1,
			},
			CamShake = {
				true,
				{5, 15, 0.1, 1},
				10,
			},
			Jumpscare = {
				true, -- Enabled ('false' if you don't want jumpscare)
				{
					Image1 = "rbxassetid://11394027278", -- Image1 url
					Image2 = "rbxassetid://11395249153", -- Image2 url
					Shake = true,
					Sound1 = {
						10483790459, -- SoundId
						{ Volume = 0.5 }, -- Sound properties
					},
					Sound2 = {
						10483837590, -- SoundId
						{ Volume = 0.5 }, -- Sound properties
					},
					Flashing = {
						true, -- Enabled
						Color3.fromRGB(48, 25, 52), -- Color
					},
					Tease = {
						false, -- Enabled ('false' if you don't want tease)
						Min = 1,
						Max = 1,
					},
				},
			},
			CustomDialog = {"You died to who you call Silence","Stay as silent as possible when you suspect its coming, so you know when to hide!","Its slow, but hard to hear","so hide!" }
		})

		local cameraShaker = require(game.ReplicatedStorage.CameraShaker)
		local camera = workspace.CurrentCamera

		local camShake = cameraShaker.new(Enum.RenderPriority.Camera.Value, function(cf)
			camera.CFrame = camera.CFrame * cf
		end)
		-----[[ Advanced ]]-----
		entity.Debug.OnEntitySpawned = function(entityModel)

		end

		entity.Debug.OnEntityDespawned = function(entityModel)
			if getgenv().death == false then
				getgenv().Title = "Eyes Closed Ears open" --Title Here
				getgenv().Description = "Stay silent or I wont be heard" --Description Here
				getgenv().Reason = "Encounter Silence" --Reason Here
				getgenv().BadgeId = 2129524598  --Replace Number with Your Badge ID
				getgenv().Category = 10 --You can replace the Category or dont

				local Unlock = require(game.Players.LocalPlayer.PlayerGui.MainUI.Initiator.Main_Lobby.RemoteListener.Modules.AchievementUnlock)
				local Achievements = debug.getupvalue(Unlock, 1)
				for i,v in pairs(require(game:GetService("ReplicatedStorage").Achievements)) do
					v.Title = getgenv().Title
					v.Desc = getgenv().Description
					v.Reason = getgenv().Reason
					v.BadgeId = getgenv().BadgeId
					v.Category = getgenv().Category
				end
				Unlock(nil,"Join")
			end
		end

		entity.Debug.OnEntityStartMoving = function(entityModel)

		end

		entity.Debug.OnEntityFinishedRebound = function(entityModel)

		end

		entity.Debug.OnDeath = function()
			getgenv().death = true
		end
		---------------------------
		-- Run the created entity
		Creator.runEntity(entity)
	end
end)

