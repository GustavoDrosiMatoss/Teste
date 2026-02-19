-- Decompiled with Konstant V2.1, a fast Luau decompiler made in Luau by plusgiant5 (https://discord.gg/brNTY8nX8t)
-- Decompiled on 2026-02-19 15:37:55
-- Luau version 6, Types version 3
-- Time taken: 0.039672 seconds

local any_new_result1 = require(game.ReplicatedStorage.Modules.Component).new({
	Tag = "PvpSessionComponent";
	Ancestors = {game.Players.LocalPlayer};
})
local tbl_14_upvr = {
	Bronze = Color3.new(0.811765, 0.6, 0.262745);
	Silver = Color3.new(0.768627, 0.768627, 0.768627);
	Gold = Color3.new(0.898039, 0.74902, 0);
	Platinum = Color3.new(0.717647, 0.952941, 1);
	Diamond = Color3.new(0.160784, 0.482353, 1);
	Master = Color3.new(0.745098, 0.431373, 1);
}
local function formatRankColor_upvr(arg1) -- Line 21, Named "formatRankColor"
	--[[ Upvalues[1]:
		[1]: tbl_14_upvr (readonly)
	]]
	for i, v in tbl_14_upvr do
		if arg1:find(i) then
			return `<font color="rgb({math.floor(v.R * 255)},{math.floor(v.G * 255)},{math.floor(v.B * 255)})">{arg1}</font>`
		end
	end
end
local function setAttributeHandler_upvr(arg1, arg2, arg3) -- Line 30, Named "setAttributeHandler"
	arg1.Maid:GiveTask(arg1.Instance:GetAttributeChangedSignal(arg2):Connect(function() -- Line 31
		--[[ Upvalues[3]:
			[1]: arg3 (readonly)
			[2]: arg1 (readonly)
			[3]: arg2 (readonly)
		]]
		arg3(arg1.Instance:GetAttribute(arg2))
	end))
	arg3(arg1.Instance:GetAttribute(arg2))
end
function any_new_result1.SetSpectating(arg1) -- Line 36
end
function any_new_result1.SteppedUpdate(arg1) -- Line 40
	if arg1.numSpectators and 0 < arg1.numSpectators then
		arg1.CameraEvent:FireServer(CFrame.new(workspace.CurrentCamera.CameraSubject.RootPart.CFrame.Position):ToObjectSpace(workspace.CurrentCamera.CFrame))
	end
end
local function _(arg1) -- Line 50, Named "formatTime"
	return string.format("%01d:%02d", math.floor(arg1 / 60), arg1 % 60)
end
local function _(arg1) -- Line 55, Named "formatTime2"
	local var9 = arg1 % 60
	local floored = math.floor(var9)
	return string.format("%01d:%02d.%03d", math.floor(arg1 / 60), floored, math.floor((var9 - floored) * 1000))
end
function any_new_result1.SetPlayerToSpectate(arg1, arg2) -- Line 64
	arg1.Maid.SpectatingCFrameConnection = nil
	if not arg2 then
	else
		local var12_upvw
		local var13_upvw
		arg1.Maid.SpectatingCFrameConnection = function() -- Line 69
			--[[ Upvalues[2]:
				[1]: var12_upvw (read and write)
				[2]: var13_upvw (read and write)
			]]
			var12_upvw:Disconnect()
			var13_upvw:Disconnect()
		end
		local var14_upvw
		var12_upvw = arg1.CameraEvent.OnClientEvent:Connect(function(arg1_2) -- Line 78
			--[[ Upvalues[1]:
				[1]: var14_upvw (read and write)
			]]
			var14_upvw = arg1_2
		end)
		local var17_upvw
		local HumanoidRootPart_upvr = arg2.Character.HumanoidRootPart
		var13_upvw = game:GetService("RunService").RenderStepped:Connect(function() -- Line 82
			--[[ Upvalues[3]:
				[1]: var17_upvw (read and write)
				[2]: var14_upvw (read and write)
				[3]: HumanoidRootPart_upvr (readonly)
			]]
			if not var17_upvw then
				if var14_upvw then
					var17_upvw = var14_upvw
				else
					return
				end
			end
			var17_upvw = var17_upvw:Lerp(var14_upvw, 0.9)
			if var17_upvw ~= var17_upvw then
				var17_upvw = var14_upvw
			end
			workspace.CurrentCamera.CFrame = CFrame.new(HumanoidRootPart_upvr.CFrame.Position):ToWorldSpace(var17_upvw)
		end)
	end
end
local function var19_upvw(arg1) -- Line 98
	local clone_5_upvr = script.ContinueScreen:Clone()
	task.spawn(function() -- Line 100
		--[[ Upvalues[2]:
			[1]: clone_5_upvr (readonly)
			[2]: arg1 (readonly)
		]]
		clone_5_upvr.Parent = game.Players.LocalPlayer.PlayerGui
		clone_5_upvr.Exit.Activated:Connect(function() -- Line 102
			--[[ Upvalues[1]:
				[1]: arg1 (copied, readonly)
			]]
			arg1.Instance:FireServer("Exit")
		end)
	end)
	return clone_5_upvr
end
function ApplyHpBar(arg1, arg2, arg3) -- Line 109
	local maximum = math.max(1, arg3 + 1)
	local var24
	local var25
	if 1 < maximum then
		local rounded = math.floor(arg1.AbsoluteSize.X * (arg3 + arg2) / maximum + 0.5)
		var24 = math.floor(arg2 / (arg2 + arg3) * rounded)
		var25 = rounded - var24
	else
		var24 = math.floor(arg1.AbsoluteSize.X * arg2 + 0.5)
		var25 = math.floor(arg1.AbsoluteSize.X * arg3 + 0.5)
	end
	arg1.Fill.Size = UDim2.new(0, var24, 1, 0)
	if 0 < arg3 then
		arg1.OverFill.Visible = true
		arg1.OverFill.Size = UDim2.new(0, var25, 1, 0)
		arg1.OverFill.Position = UDim2.fromOffset(var24, 0)
	else
		arg1.OverFill.Visible = false
	end
end
function any_new_result1.DisplayEndGameStats2v2(arg1, arg2, arg3) -- Line 170
	--[[ Upvalues[1]:
		[1]: formatRankColor_upvr (readonly)
	]]
	-- KONSTANTERROR: [0] 1. Error Block 1 start (CF ANALYSIS FAILED)
	print(arg2, arg3)
	local function _(arg1_6) -- Line 172, Named "commaNumber"
		local var98
		repeat
			local string_gsub_result1_2, string_gsub_result2 = string.gsub(var98, "^(-?%d+)(%d%d%d)", "%1,%2")
			var98 = string_gsub_result1_2
		until string_gsub_result2 == 0
		return var98
	end
	-- KONSTANTERROR: [0] 1. Error Block 1 end (CF ANALYSIS FAILED)
	-- KONSTANTERROR: [14] 13. Error Block 3 start (CF ANALYSIS FAILED)
	-- KONSTANTERROR: [14] 13. Error Block 3 end (CF ANALYSIS FAILED)
	-- KONSTANTERROR: [11] 11. Error Block 131 start (CF ANALYSIS FAILED)
	if nil ~= "2v2" then return end
	local clone_4 = script.PvPEventResult:Clone()
	local Main_2 = clone_4.Modal.Main
	local tbl_2 = {}
	for _, v_2 in Main_2.Players:GetChildren() do
		if v_2:IsA("Frame") then
			local children_2 = v_2:GetChildren()
			table.insert(tbl_2, {v_2, children_2})
			table.sort(children_2, function(arg1_7, arg2_4) -- Line 202
				local var110
				if arg1_7.Name >= arg2_4.Name then
					var110 = false
				else
					var110 = true
				end
				return var110
			end)
		end
	end
	table.sort(tbl_2, function(arg1_8, arg2_5) -- Line 208
		local var112
		if arg1_8[1].Name >= arg2_5[1].Name then
			var112 = false
		else
			var112 = true
		end
		return var112
	end)
	local TextLabel_2 = Main_2.Header.TextLabel
	if arg2[game.Players.LocalPlayer.Name].Stats.Winner then
		TextLabel_2.Text = "Victory!"
		TextLabel_2.DefeatUIGradient:Destroy()
		TextLabel_2.VictoryUIGradient.Enabled = true
	else
		TextLabel_2.Text = "Defeat.."
		TextLabel_2.VictoryUIGradient:Destroy()
		TextLabel_2.DefeatUIGradient.Enabled = true
	end
	local var115 = arg3.EndingTime - arg3.StartTime
	Main_2.Header.Timer.Text = `Match Time: {string.format("%01d:%02d", math.floor(var115 / 60), var115 % 60)}`
	local tbl_8 = {}
	local tbl_13 = {
		TotalDamage = {};
		FruitDmg = {};
		MeleeDmg = {};
		SwordDmg = {};
		GunDmg = {};
		Kills = {};
		DamageTanked = {};
	}
	for i_3, v_3 in arg2 do
		local var118 = game.Players[i_3]
		local Stats_2 = v_3.Stats
		local TeamId_2 = v_3.TeamId
		local _2_2 = tbl_2[TeamId_2][2]
		local popped_2 = table.remove(_2_2, 1)
		local var123
		if 0 < #tbl_2[TeamId_2][2] then
			_2_2 = 1
		else
			_2_2 = 2
		end
		if not popped_2 then
			error("grr")
		end
		local Portrait = popped_2.Portrait
		var123 = `https://www.roblox.com/headshot-thumbnail/image?userId={var118.UserId}&width=420&height=420&format=png`
		Portrait.Image.Image = var123
		if Stats_2.Winner then
			var123 = true
		else
			var123 = false
		end
		Portrait.WinIcon.Visible = var123
		if v_3.Dead then
			-- KONSTANTWARNING: GOTO [243] #163
		end
		Portrait.DeathIcon.Visible = false
		if Stats_2.Winner then
		else
		end
		Portrait.StatusGradient.BackgroundColor3 = Color3.fromRGB(161, 35, 35)
		popped_2.Username.Text = var118.DisplayName
		v_3.TeamFrameId = TeamId_2
		v_3.PlayerFrameId = _2_2
		print("FreeFrame", popped_2, TeamId_2, _2_2)
		tbl_8[`T{TeamId_2}P{_2_2}`] = v_3
		tbl_8[v_3] = `T{TeamId_2}P{_2_2}`
		v_3.AchievementLabel = popped_2.Achievement
		v_3.AchievementLabel.Text = ""
		table.insert(tbl_13.TotalDamage, {v_3, Stats_2.DamageDealt.Fruit + Stats_2.DamageDealt.Gun + Stats_2.DamageDealt.Melee + Stats_2.DamageDealt.Sword})
		table.insert(tbl_13.FruitDmg, {v_3, Stats_2.DamageDealt.Fruit})
		table.insert(tbl_13.GunDmg, {v_3, Stats_2.DamageDealt.Gun})
		table.insert(tbl_13.MeleeDmg, {v_3, Stats_2.DamageDealt.Melee})
		table.insert(tbl_13.SwordDmg, {v_3, Stats_2.DamageDealt.Sword})
		table.insert(tbl_13.Kills, {v_3, Stats_2.Kills})
		local tbl_10 = {v_3, Stats_2.DamageTaken}
		table.insert(tbl_13.DamageTanked, tbl_10)
	end
	for _, v_4 in clone_4:GetDescendants() do
		if v_4.Name:find("StatTextLabel") then
			warn("found", v_4:GetFullName())
			v_4.Text = '-'
		end
	end
	local Statistics = clone_4.Modal.Main.Statistics
	for i_5, v_5 in tbl_8 do
		if typeof(i_5) == "string" then
			Statistics.RankChange[i_5.."StatTextLabel"].Text = formatRankColor_upvr(v_5.NewRankName)
			Statistics.RankChange[i_5.."StatTextLabel"].TextColor3 = Color3.new(1, 1, 1)
			Statistics.RankChange[i_5.."StatTextLabel"].RichText = true
			if v_5.NewRankName == "Master" then
				tbl_10 = v_5.NewRankName
				local var136 = tbl_10
				if 0 < v_5.MMRChange then
					var136 = '+'
				else
					var136 = '-'
				end
				Statistics.RankChange[i_5.."StatTextLabel"].Text = `{formatRankColor_upvr(var136)} {var136}{v_5.MMRChange}BP`
			end
		end
	end
	-- KONSTANTERROR: [11] 11. Error Block 131 end (CF ANALYSIS FAILED)
end
local any_getLogAppendWrapper_result1_upvr = require(game.ReplicatedStorage.Util.IrisLog).new("PvpDirector", 2):getLogAppendWrapper(script, true)
local Maid_upvr = require(game.ReplicatedStorage.Util.Maid)
function any_new_result1.Start(arg1) -- Line 414
	--[[ Upvalues[4]:
		[1]: any_getLogAppendWrapper_result1_upvr (readonly)
		[2]: Maid_upvr (readonly)
		[3]: setAttributeHandler_upvr (readonly)
		[4]: var19_upvw (read and write)
	]]
	any_getLogAppendWrapper_result1_upvr(`PvpSessionComponent constructed for LocalPlayer ({arg1.Instance:GetFullName()})`)
	arg1.Maid = Maid_upvr.new()
	arg1.CameraEvent = arg1.Instance:WaitForChild("CameraEvent", 99)
	setAttributeHandler_upvr(arg1, "State", function(arg1_9) -- Line 420
		--[[ Upvalues[2]:
			[1]: arg1 (readonly)
			[2]: var19_upvw (copied, read and write)
		]]
		if arg1_9 == "Waiting" then
			arg1.Maid.CancelButton = var19_upvw(arg1)
		else
			if arg1_9 == "Playing" then
				arg1.Maid.CancelButton = nil
				return
			end
			arg1.Maid.CancelButton = nil
		end
	end)
	setAttributeHandler_upvr(arg1, "Spectators", function(arg1_10) -- Line 429
		--[[ Upvalues[2]:
			[1]: any_getLogAppendWrapper_result1_upvr (copied, readonly)
			[2]: arg1 (readonly)
		]]
		any_getLogAppendWrapper_result1_upvr(`Spectators changing: {arg1_10}`)
		arg1.numSpectators = arg1_10 or 0
	end)
	arg1.Maid:GiveTask(function() -- Line 433
		game.Players.LocalPlayer.PlayerGui.Backpack.Enabled = true
	end)
	local var142_upvw
	local function setSpectate_upvr(arg1_11) -- Line 436, Named "setSpectate"
		--[[ Upvalues[3]:
			[1]: var142_upvw (read and write)
			[2]: arg1 (readonly)
			[3]: any_getLogAppendWrapper_result1_upvr (copied, readonly)
		]]
		var142_upvw = arg1_11
		arg1.Maid.BackpackTask = task.delay(0.1, function() -- Line 438
			--[[ Upvalues[1]:
				[1]: var142_upvw (copied, read and write)
			]]
			if not var142_upvw then
				game.Players.LocalPlayer.PlayerGui.Backpack.Enabled = true
			else
				game.Players.LocalPlayer.PlayerGui.Backpack.Enabled = false
			end
		end)
		any_getLogAppendWrapper_result1_upvr(`Spectating: {arg1_11}`)
		if not arg1_11 then
			arg1:SetPlayerToSpectate(nil)
		else
			arg1:SetPlayerToSpectate(game.Players:FindFirstChild(arg1_11))
		end
	end
	setAttributeHandler_upvr(arg1, "Spectating", setSpectate_upvr)
	setAttributeHandler_upvr(arg1, "ShowEndStatsScreen", function(arg1_12) -- Line 453
		--[[ Upvalues[2]:
			[1]: setSpectate_upvr (readonly)
			[2]: arg1 (readonly)
		]]
		if not arg1_12 then
		else
			pcall(function() -- Line 455
				--[[ Upvalues[2]:
					[1]: setSpectate_upvr (copied, readonly)
					[2]: arg1_12 (readonly)
				]]
				setSpectate_upvr(arg1_12)
			end)
			arg1.Instance.OnClientEvent:Connect(function(arg1_13, arg2, arg3) -- Line 459
				--[[ Upvalues[1]:
					[1]: arg1 (copied, readonly)
				]]
				print("RECEIVER", arg1_13, arg2, arg3)
				if arg1_13 == "EndGameStats" then
					arg1:DisplayEndGameStats2v2(arg2, arg3)
				end
			end)
		end
	end)
	setAttributeHandler_upvr(arg1, "MatchEndTime", function(arg1_14) -- Line 467
		--[[ Upvalues[1]:
			[1]: arg1 (readonly)
		]]
		if not arg1_14 then
			arg1.Maid.matchTimer = nil
		else
			task.wait(1)
			arg1.Maid.matchTimer = task.spawn(function() -- Line 473
				--[[ Upvalues[2]:
					[1]: arg1 (copied, readonly)
					[2]: arg1_14 (readonly)
				]]
				repeat
					task.wait()
				until arg1.pvpHud
				arg1.matchEndTime = arg1_14
				while task.wait() do
					local var149 = arg1_14 - workspace:GetServerTimeNow()
					if 10 < var149 then
						arg1.pvpHud.matchTimer.Text = string.format("%01d:%02d", math.floor(var149 / 60), var149 % 60)
					elseif var149 < 0 then
						local absolute = math.abs(var149)
						local var151 = absolute % 60
						local floored_4 = math.floor(var151)
						arg1.pvpHud.matchTimer.Text = '+'..string.format("%01d:%02d.%03d", math.floor(absolute / 60), floored_4, math.floor((var151 - floored_4) * 1000))
					else
						arg1.pvpHud.matchTimer.TextColor3 = Color3.new(1, 0.34902, 0.34902)
						local var153 = var149 % 60
						local floored_3 = math.floor(var153)
						arg1.pvpHud.matchTimer.Text = string.format("%01d:%02d.%03d", math.floor(var149 / 60), floored_3, math.floor((var153 - floored_3) * 1000))
					end
				end
			end)
		end
	end)
	setAttributeHandler_upvr(arg1, "MatchStartTimer", function(arg1_15) -- Line 490
		--[[ Upvalues[1]:
			[1]: arg1 (readonly)
		]]
		if not arg1_15 then
			arg1.Maid.matchTimer = nil
		else
			arg1.Maid.matchTimer = task.spawn(function() -- Line 495
				--[[ Upvalues[2]:
					[1]: arg1 (copied, readonly)
					[2]: arg1_15 (readonly)
				]]
				repeat
					task.wait()
				until arg1.pvpHud
				arg1.matchEndTime = arg1_15
				while task.wait() do
					local var157 = arg1_15 - workspace:GetServerTimeNow()
					if 10 < var157 then
						arg1.pvpHud.matchTimer.Text = string.format("%01d:%02d", math.floor(var157 / 60), var157 % 60)
					elseif var157 < 0 then
						arg1.pvpHud.matchTimer.Text = "FIGHT!"
					else
						arg1.pvpHud.matchTimer.TextColor3 = Color3.new(1, 0.34902, 0.34902)
						local var158 = var157 % 60
						local floored_2 = math.floor(var158)
						arg1.pvpHud.matchTimer.Text = string.format("%01d:%02d.%03d", math.floor(var157 / 60), floored_2, math.floor((var158 - floored_2) * 1000))
					end
				end
			end)
		end
	end)
	setAttributeHandler_upvr(arg1, "OutOfBounds", function(arg1_16) -- Line 512
		--[[ Upvalues[1]:
			[1]: arg1 (readonly)
		]]
		-- KONSTANTERROR: [0] 1. Error Block 1 start (CF ANALYSIS FAILED)
		-- KONSTANTERROR: [0] 1. Error Block 1 end (CF ANALYSIS FAILED)
		-- KONSTANTERROR: [5] 5. Error Block 3 start (CF ANALYSIS FAILED)
		local returnAlert_upvr = arg1.pvpHud.returnAlert
		local task_spawn_result1_upvr = task.spawn(function() -- Line 516
			--[[ Upvalues[2]:
				[1]: arg1 (copied, readonly)
				[2]: returnAlert_upvr (readonly)
			]]
			local var164 = game.Players.LocalPlayer.Character
			if var164 then
				var164 = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
			end
			if not var164 or var164.Health <= 0 then
				arg1.Maid.OutOfBoundsScreen = nil
			else
				while true do
					if not task.wait() then break end
					returnAlert_upvr.TextTransparency = math.lerp(1, 0, math.clamp((tick() - tick()) / 2, 0, 1))
					returnAlert_upvr.TextColor3 = Color3.fromHSV(0, 0.9, math.sin(os.clock() % 1 / 1 * math.pi * 2) * 0.5 + 0.5)
				end
			end
		end)
		arg1.Maid.OutOfBoundsScreen = function() -- Line 533
			--[[ Upvalues[2]:
				[1]: task_spawn_result1_upvr (readonly)
				[2]: returnAlert_upvr (readonly)
			]]
			pcall(task.cancel, task_spawn_result1_upvr)
			returnAlert_upvr.TextTransparency = 1
		end
		do
			return
		end
		-- KONSTANTERROR: [5] 5. Error Block 3 end (CF ANALYSIS FAILED)
		-- KONSTANTERROR: [25] 20. Error Block 4 start (CF ANALYSIS FAILED)
		task_spawn_result1_upvr = arg1
		returnAlert_upvr = task_spawn_result1_upvr.Maid
		task_spawn_result1_upvr = nil
		returnAlert_upvr.OutOfBoundsScreen = task_spawn_result1_upvr
		-- KONSTANTERROR: [25] 20. Error Block 4 end (CF ANALYSIS FAILED)
	end)
	local pvpArenaPointer = arg1.Instance:WaitForChild("pvpArenaPointer", 100)
	if pvpArenaPointer.Value then
		local Value_3 = pvpArenaPointer.Value
		local TeamId_3_upvr = arg1.Instance:GetAttribute("TeamId")
		local function handlePvpInfoAdded_upvr(arg1_17) -- Line 548, Named "handlePvpInfoAdded"
			--[[ Upvalues[3]:
				[1]: arg1 (readonly)
				[2]: TeamId_3_upvr (readonly)
				[3]: any_getLogAppendWrapper_result1_upvr (copied, readonly)
			]]
			local clone_3_upvr = script.PvpHUD:Clone()
			arg1.Maid:GiveTask(clone_3_upvr)
			arg1.pvpHud = clone_3_upvr
			clone_3_upvr.Parent = game.Players.LocalPlayer.PlayerGui
			local function handlePvpTeamInfoAdded_upvr(arg1_18) -- Line 554, Named "handlePvpTeamInfoAdded"
				--[[ Upvalues[4]:
					[1]: TeamId_3_upvr (copied, readonly)
					[2]: any_getLogAppendWrapper_result1_upvr (copied, readonly)
					[3]: clone_3_upvr (readonly)
					[4]: arg1 (copied, readonly)
				]]
				-- KONSTANTWARNING: Variable analysis failed. Output will have some incorrect variable assignments
				local var183_upvr
				if arg1_18.Name ~= tostring(TeamId_3_upvr) then
					var183_upvr = false
				else
					var183_upvr = true
				end
				local function pvpPlayerInfoAdded_upvr(arg1_19) -- Line 556, Named "pvpPlayerInfoAdded"
					--[[ Upvalues[3]:
						[1]: any_getLogAppendWrapper_result1_upvr (copied, readonly)
						[2]: clone_3_upvr (copied, readonly)
						[3]: var183_upvr (readonly)
					]]
					any_getLogAppendWrapper_result1_upvr(`HealthBar Added: {arg1_19.Value}`)
					local clone_2_upvr = clone_3_upvr.Folder.HP:Clone()
					local Value = arg1_19.Value
					clone_2_upvr.NameLabel.Text = `{Value.DisplayName}`
					local function onHealthUpdated_upvr(arg1_21, arg2) -- Line 562, Named "onHealthUpdated"
						--[[ Upvalues[1]:
							[1]: clone_2_upvr (readonly)
						]]
						if not clone_2_upvr:FindFirstChild("HpLabel") then
						else
							clone_2_upvr.HpLabel.Text = `{math.round(arg1_21 / arg2 * 100)}%`
							ApplyHpBar(clone_2_upvr, arg1_21 / arg2, 0)
							if arg1_21 <= 0 then
								clone_2_upvr.HpLabel.Text = "ELIMINATED"
								clone_2_upvr.Fill.BackgroundColor3 = Color3.fromRGB(109, 109, 109)
								clone_2_upvr.Fill.Trans.BackgroundColor3 = Color3.fromRGB(56, 56, 56)
							end
						end
					end
					if not var183_upvr then
						clone_2_upvr.Parent = clone_3_upvr.HealthBarsEnemy
						clone_2_upvr.Fill.BackgroundColor3 = Color3.fromRGB(255, 59, 0)
						clone_2_upvr.Fill.Trans.BackgroundColor3 = Color3.fromRGB(198, 26, 0)
					else
						clone_2_upvr.Parent = clone_3_upvr.HealthBarsAlly
					end
					local Character_2 = Value.Character
					if Character_2 then
						local Humanoid_upvr_2 = Character_2:FindFirstChild("Humanoid")
						if Humanoid_upvr_2 then
							onHealthUpdated_upvr(Humanoid_upvr_2.Health, Humanoid_upvr_2.MaxHealth)
							Humanoid_upvr_2.HealthChanged:Connect(function() -- Line 586
								--[[ Upvalues[2]:
									[1]: onHealthUpdated_upvr (readonly)
									[2]: Humanoid_upvr_2 (readonly)
								]]
								onHealthUpdated_upvr(Humanoid_upvr_2.Health, Humanoid_upvr_2.MaxHealth)
							end)
						end
					end
					Humanoid_upvr_2 = true
					clone_2_upvr.Visible = Humanoid_upvr_2
				end
				arg1.Maid:GiveTask(arg1_18.ChildAdded:Connect(function(arg1_22) -- Line 595
					--[[ Upvalues[1]:
						[1]: pvpPlayerInfoAdded_upvr (readonly)
					]]
					pvpPlayerInfoAdded_upvr(arg1_22)
				end))
				for _, v_6 in arg1_18:GetChildren() do
					pvpPlayerInfoAdded_upvr(v_6)
					local _
				end
			end
			arg1.Maid:GiveTask(arg1_17.ChildAdded:Connect(function(arg1_23) -- Line 599
				--[[ Upvalues[1]:
					[1]: handlePvpTeamInfoAdded_upvr (readonly)
				]]
				handlePvpTeamInfoAdded_upvr(arg1_23)
			end))
			for _, v_7 in arg1_17:GetChildren() do
				handlePvpTeamInfoAdded_upvr(v_7)
			end
		end
		i