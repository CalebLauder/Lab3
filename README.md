# Save System From my Tier List game on Roblox.com. (Server Side



local DataStoreService = game:GetService("DataStoreService")
local SaveSlot1 = DataStoreService:GetDataStore("SaveSlot1")
local SaveSlot2 = DataStoreService:GetDataStore("SaveSlot2")
local SaveSlot3 = DataStoreService:GetDataStore("SaveSlot3")
local Players = game:GetService("Players")
local Rep = game:GetService("ReplicatedStorage")
local SaveLoadFolder = Rep.SaveLoad
local UpdateSave1 = SaveLoadFolder.Save1
local UpdateSave2 = SaveLoadFolder.Save2
local UpdateSave3 = SaveLoadFolder.Save3

local UpdatePlayerTitle = SaveLoadFolder.UpdateTitle


Players.PlayerAdded:Connect(function(player)
	local PlayerID = "Player_"..player.UserId
	local TierList1
	local success, errormessage = pcall(function()
		TierList1 = SaveSlot1:GetAsync(PlayerID)
		
	end)
	
	if success then 
		
		UpdateSave1:FireClient(player, TierList1)
	end
	
	
	
	local TierList2
	local success, errormessage = pcall(function()
		TierList2 = SaveSlot2:GetAsync(PlayerID)

	end)

	if success then 

		UpdateSave2:FireClient(player,TierList2)
	end
	
	
	
	local TierList3
	local success, errormessage = pcall(function()
		TierList3 = SaveSlot3:GetAsync(PlayerID)

	end)

	if success then 

		UpdateSave3:FireClient(player, TierList3)
	end

end)


Players.PlayerAdded:Connect(function(player)
	local PlayerID = "Player_"..player.UserId
	
end)


Players.PlayerAdded:Connect(function(player)
	local PlayerID = "Player_"..player.UserId
	

end)



UpdateSave1.OnServerEvent:Connect(function(Plr, Dictionary)
	print("Updated")
	local PlayerID = "Player_"..Plr.UserId
	local success, errormessage = pcall(function()
		SaveSlot1:SetAsync(PlayerID, Dictionary)
	end)
	
	if success then 
		
	else
		print("Error")
		warn(errormessage)
	end
	
end)

UpdateSave2.OnServerEvent:Connect(function(Plr, Dictionary)
	print("Updated")
	local PlayerID = "Player_"..Plr.UserId
	local success, errormessage = pcall(function()
		SaveSlot2:SetAsync(PlayerID, Dictionary)
	end)

	if success then 

	else
		print("Error")
		warn(errormessage)
	end
	
end)

UpdateSave3.OnServerEvent:Connect(function(Plr, Dictionary)
	print("Updated")
	
	local PlayerID = "Player_"..Plr.UserId
	local success, errormessage = pcall(function()
		SaveSlot3:SetAsync(PlayerID, Dictionary)
	end)

	if success then 

	else
		print("Error")
		warn(errormessage)
	end
	
end)


UpdatePlayerTitle.OnServerEvent:Connect(function(Player, Title)
	Player:WaitForChild("TierListTitle").Value = Title
end)

