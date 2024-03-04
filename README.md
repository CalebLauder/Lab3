# Save System From my Tier List game on Roblox.com. (Client Side)
#For one of three, this example is the client side script for Save1.


local Whole = script.Parent.Parent.Whole

local STier = Whole.Tiers:FindFirstChild("STier")
local ATier = Whole.Tiers:FindFirstChild("ATier")
local BTier  = Whole.Tiers:FindFirstChild("BTier")
local CTier  = Whole.Tiers:FindFirstChild("CTier")
local DTier  = Whole.Tiers:FindFirstChild("DTier")
local DTier  = Whole.Tiers:FindFirstChild("DTier")
local FTier = Whole.Tiers:FindFirstChild('FTier')
local ScrollingFrame = Whole.Parent.ScrollingFrame
local TierListTitle = Whole.Parent.Outside.TextBox


local SaveButton1 = script.Parent.Save1
local LoadButton1 = script.Parent.Load1
local S = {}
local A = {}
local B = {}
local C = {}
local D = {}
local F = {}
local ScrollData = {}


local Player = game:GetService("Players").LocalPlayer
local PlayerTitle = Player:WaitForChild("TierListTitle")

local Rep = game:GetService("ReplicatedStorage")
local SaveLoadFolder = Rep.SaveLoad
local UpdatePlayerTitle = SaveLoadFolder.UpdateTitle

local Save1Event = SaveLoadFolder.Save1

local Save1LabelText = script.Parent.One
local Save1 = nil

local function CLEARTHETABLES()
	table.clear(S)
	table.clear(A)
	table.clear(B)
	table.clear(C)
	table.clear(D)
	table.clear(F)
	table.clear(ScrollData)
end


local function FillTheTables()
	
	
	for i, Image in pairs(STier:GetChildren()) do

		if Image:IsA("ImageButton") then 
			table.insert(S,Image.Image) 

		end
	end
	
	for i, Image in pairs(ATier:GetChildren()) do

		if Image:IsA("ImageButton") then 
			table.insert(A,Image.Image) 

		end
	end
	
	for i, Image in pairs(BTier:GetChildren()) do

		if Image:IsA("ImageButton") then 
			table.insert(B,Image.Image) 

		end
	end
	for i, Image in pairs(CTier:GetChildren()) do

		if Image:IsA("ImageButton") then 
			table.insert(C,Image.Image) 

		end
	end
	for i, Image in pairs(DTier:GetChildren()) do

		if Image:IsA("ImageButton") then 
			table.insert(D,Image.Image) 

		end
	end
	for i, Image in pairs(FTier:GetChildren()) do

		if Image:IsA("ImageButton") then 
			table.insert(F,Image.Image) 

		end
	end
	
	for i , Image in pairs(ScrollingFrame:GetChildren()) do
		if Image:IsA("ImageButton") then 
			table.insert(ScrollData,Image.Image) 

		end
	end
	
	
end




local function Save (NumberSaved)
	
	CLEARTHETABLES()
	FillTheTables()
	
	local DictionaryOfTemplates = {
		["Title"] = PlayerTitle.Value,
		["S"] = S,
		["A"] = A,
		["B"] = B,
		["C"] = C,
		["D"] = D,	
		["F"] = F,
		["ScrollFrame"] = ScrollData
	}
    
	Save1Event:FireServer(DictionaryOfTemplates)

	Save1 = DictionaryOfTemplates
	
	if DictionaryOfTemplates.Title ~= nil then
		Save1LabelText.Text = "Save Slot #1: "..DictionaryOfTemplates.Title
	end

end

SaveButton1.MouseButton1Up:Connect(function()
	Save(SaveButton1.Name)
	
end)

Save1Event.OnClientEvent:Connect(function(Dictionary)
	Save1 = Dictionary
	

	if Dictionary.Title ~= nil then
		Save1LabelText.Text = "Save Slot #1: "..Dictionary.Title

	else 
		Save1LabelText.Text = "Save Slot #1: Empty"
	end


  
end)



------------------------------------------------

local AddedToTierEvents = Rep.AddedToTierEvents


local function ClearWhole() 	
	local TierFolder = Whole.Tiers

	for i, Tier in pairs(TierFolder:GetChildren()) do
		for h, Image in pairs(Tier:GetChildren()) do
			if Image:IsA("ImageButton") then
				Image:Destroy()
			end



		end
	end
end



LoadButton1.MouseButton1Up:Connect(function() 
	
	local ClonedImage = Rep:WaitForChild("ClonedImageTier")
	local ClonedImageScroll = Rep:WaitForChild("ClonedImageScroll")
	local Clear = AddedToTierEvents.Clear:FireServer()

	if Save1 ~= {} then
		if Save1.Title ~= nil then
			TierListTitle.Text = Save1.Title
			UpdatePlayerTitle:FireServer(Save1.Title)

		else 
			Save1LabelText.Text = "Save Slot #3: Empty"
		end


		ClearWhole()
		
		for i, Image in pairs(ScrollingFrame:GetChildren()) do
			if Image:IsA("ImageButton") then
				Image:Destroy()
			end
		end
		
		for i, v in pairs(Save1.ScrollFrame) do
			local Image = ClonedImageScroll:Clone()
			Image.Parent = ScrollingFrame
			Image.Image = v
			Image.Name = v
			
			
		end
		for i, v in pairs(Save1.S) do
			local Image = ClonedImage:Clone()
			Image.Parent = STier
			Image.Image = v
			Image.Name = v
			AddedToTierEvents.STier:FireServer(Image.Image)
		end
		
		for i, v in pairs(Save1.A) do
			local Image = ClonedImage:Clone()
			Image.Parent = ATier
			Image.Image = v
			Image.Name = v
			AddedToTierEvents.ATier:FireServer(Image.Image)
		end
		for i, v in pairs(Save1.B) do
			local Image = ClonedImage:Clone()
			Image.Parent = BTier
			Image.Image = v
			Image.Name = v
			AddedToTierEvents.BTier:FireServer(Image.Image)
		end
		for i, v in pairs(Save1.C) do
			local Image = ClonedImage:Clone()
			Image.Parent = CTier
			Image.Image = v
			Image.Name = v
			AddedToTierEvents.CTier:FireServer(Image.Image)
		end
		for i, v in pairs(Save1.D) do
			local Image = ClonedImage:Clone()
			Image.Parent = DTier
			Image.Image = v
			Image.Name = v
			AddedToTierEvents.DTier:FireServer(Image.Image)
		end
		for i, v in pairs(Save1.F) do
			local Image = ClonedImage:Clone()
			Image.Parent = FTier
			Image.Image = v
			Image.Name = v
			AddedToTierEvents.FTier:FireServer(Image.Image)
		end
	end
end)


