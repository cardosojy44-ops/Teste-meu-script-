-- LocalScript (colocar em StarterGui)
-- Menu educacional / de aparência "mod menu"
-- DESCRIÇÃO: "Feito pelo Yago"
-- Atenção: Este script é educativo. Não realiza cheats nem interage com jogos alheios.

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local player = Players.LocalPlayer
local gui = Instance.new("ScreenGui")
gui.Name = "YagoModMenu"
gui.Parent = player:WaitForChild("PlayerGui")
gui.ResetOnSpawn = false

-- Main frame
local main = Instance.new("Frame")
main.Name = "MainFrame"
main.Size = UDim2.new(0, 420, 0, 320)
main.Position = UDim2.new(0.5, -210, 0.2, 0)
main.AnchorPoint = Vector2.new(0.5, 0)
main.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
main.BorderSizePixel = 0
main.Parent = gui
main.BackgroundTransparency = 0

-- Rounded corners
local corner = Instance.new("UICorner", main)
corner.CornerRadius = UDim.new(0, 12)

-- Header
local header = Instance.new("Frame")
header.Name = "Header"
header.Size = UDim2.new(1, 0, 0, 56)
header.BackgroundTransparency = 1
header.Parent = main

local title = Instance.new("TextLabel")
title.Name = "Title"
title.Size = UDim2.new(0.7, -12, 1, 0)
title.Position = UDim2.new(0, 12, 0, 0)
title.BackgroundTransparency = 1
title.Text = "Mod Menu"
title.Font = Enum.Font.GothamBold
title.TextSize = 20
title.TextColor3 = Color3.fromRGB(240,240,240)
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = header

local desc = Instance.new("TextLabel")
desc.Name = "Description"
desc.Size = UDim2.new(0.3, -12, 1, 0)
desc.Position = UDim2.new(0.7, 0, 0, 0)
desc.BackgroundTransparency = 1
desc.Text = "Feito pelo Yago"
desc.Font = Enum.Font.Gotham
desc.TextSize = 14
desc.TextColor3 = Color3.fromRGB(180,180,180)
desc.TextXAlignment = Enum.TextXAlignment.Right
desc.Parent = header

-- Minimize button
local minimizeBtn = Instance.new("TextButton")
minimizeBtn.Name = "Minimize"
minimizeBtn.Size = UDim2.new(0, 36, 0, 36)
minimizeBtn.Position = UDim2.new(1, -48, 0, 10)
minimizeBtn.AnchorPoint = Vector2.new(0, 0)
minimizeBtn.BackgroundColor3 = Color3.fromRGB(50,50,60)
minimizeBtn.Text = "—"
minimizeBtn.Font = Enum.Font.GothamBold
minimizeBtn.TextSize = 20
minimizeBtn.TextColor3 = Color3.fromRGB(240,240,240)
minimizeBtn.Parent = header
local minCorner = Instance.new("UICorner", minimizeBtn); minCorner.CornerRadius = UDim.new(0,8)

-- Close button (optional)
local closeBtn = Instance.new("TextButton")
closeBtn.Name = "Close"
closeBtn.Size = UDim2.new(0, 36, 0, 36)
closeBtn.Position = UDim2.new(1, -96, 0, 10)
closeBtn.BackgroundColor3 = Color3.fromRGB(50,50,60)
closeBtn.Text = "x"
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 16
closeBtn.TextColor3 = Color3.fromRGB(240,240,240)
closeBtn.Parent = header
local closeCorner = Instance.new("UICorner", closeBtn); closeCorner.CornerRadius = UDim.new(0,8)

-- Content area
local content = Instance.new("Frame")
content.Name = "Content"
content.Size = UDim2.new(1, -24, 1, -80)
content.Position = UDim2.new(0, 12, 0, 64)
content.BackgroundTransparency = 1
content.Parent = main

-- Left column (toggles)
local leftCol = Instance.new("Frame")
leftCol.Name = "LeftCol"
leftCol.Size = UDim2.new(0.5, -6, 1, 0)
leftCol.Position = UDim2.new(0, 0, 0, 0)
leftCol.BackgroundTransparency = 1
leftCol.Parent = content

-- Right column (buttons/info)
local rightCol = Instance.new("Frame")
rightCol.Name = "RightCol"
rightCol.Size = UDim2.new(0.5, -6, 1, 0)
rightCol.Position = UDim2.new(0.5, 6, 0, 0)
rightCol.BackgroundTransparency = 1
rightCol.Parent = content

-- Utility to create a toggle row
local function createToggle(parent, labelText, initial)
	local row = Instance.new("Frame", parent)
	row.Size = UDim2.new(1, 0, 0, 48)
	row.BackgroundTransparency = 1

	local lbl = Instance.new("TextLabel", row)
	lbl.Size = UDim2.new(0.7, 0, 1, 0)
	lbl.BackgroundTransparency = 1
	lbl.Text = labelText
	lbl.Font = Enum.Font.Gotham
	lbl.TextSize = 16
	lbl.TextColor3 = Color3.fromRGB(230,230,230)
	lbl.TextXAlignment = Enum.TextXAlignment.Left

	local toggle = Instance.new("TextButton", row)
	toggle.Size = UDim2.new(0, 84, 0, 28)
	toggle.Position = UDim2.new(1, -84, 0.5, -14)
	toggle.BackgroundColor3 = Color3.fromRGB(60,60,70)
	toggle.Text = initial and "ON" or "OFF"
	toggle.Font = Enum.Font.GothamBold
	toggle.TextColor3 = Color3.fromRGB(240,240,240)
	local tCorner = Instance.new("UICorner", toggle); tCorner.CornerRadius = UDim.new(0,8)

	-- state
	local state = initial or false

	toggle.MouseButton1Click:Connect(function()
		state = not state
		toggle.Text = state and "ON" or "OFF"
		-- Placeholder: safe action (not cheating)
		if state then
			-- exemplo de ação segura: mostrar um pequeno label temporário
			print(labelText .. " ativado (apenas simulação).")
			-- Poderia exibir um pequeno aviso visual aqui
		else
			print(labelText .. " desativado (apenas simulação).")
		end
	end)

	return row, function() return state end
end

-- Add a few toggles
local gap = 8
local y = 0
local toggles = {}
local names = {"Simular AutoFarm", "Simular ESP (visual)", "Simular Auto-Click"}
for i, name in ipairs(names) do
	local r, getter = createToggle(leftCol, name, false)
	r.Position = UDim2.new(0, 0, 0, y)
	r.Parent = leftCol
	y = y + 48 + gap
	table.insert(toggles, {name = name, get = getter})
end

-- Right column buttons
local function createButton(parent, txt)
	local b = Instance.new("TextButton", parent)
	b.Size = UDim2.new(1, 0, 0, 44)
	b.BackgroundColor3 = Color3.fromRGB(80,80,95)
	b.Text = txt
	b.Font = Enum.Font.GothamBold
	b.TextSize = 16
	b.TextColor3 = Color3.fromRGB(245,245,245)
	local c = Instance.new("UICorner", b); c.CornerRadius = UDim.new(0,8)
	return b
end

local btn1 = createButton(rightCol, "Abrir Configurações")
btn1.Position = UDim2.new(0, 0, 0, 0)
btn1.MouseButton1Click:Connect(function()
	-- Safe placeholder action
	print("Abrir configurações (simulação).")
end)

local btn2 = createButton(rightCol, "Mostrar Status")
btn2.Position = UDim2.new(0, 0, 0, 54)
btn2.MouseButton1Click:Connect(function()
	local status = {}
	for _, t in ipairs(toggles) do
		table.insert(status, t.name .. ": " .. (t.get() and "ON" or "OFF"))
	end
	local msg = table.concat(status, "\n")
	-- Mostrar um simple dialog
	local dialog = Instance.new("TextLabel", main)
	dialog.Size = UDim2.new(0.9, 0, 0, 120)
	dialog.Position = UDim2.new(0.05, 0, 0.6, 0)
	dialog.BackgroundTransparency = 0.05
	dialog.BackgroundColor3 = Color3.fromRGB(20,20,30)
	dialog.TextColor3 = Color3.fromRGB(230,230,230)
	dialog.TextWrapped = true
	dialog.Text = "Status:\n" .. msg
	local dCorner = Instance.new("UICorner", dialog); dCorner.CornerRadius = UDim.new(0,8)
	
	delay(3, function() 
		if dialog then dialog:Destroy() end
	end)
end)

local btn3 = createButton(rightCol, "Fechar Menu")
btn3.Position = UDim2.new(0, 0, 0, 108)
btn3.MouseButton1Click:Connect(function()
	main:Destroy()
end)

-- Visual polish: decorative gradient
local grad = Instance.new("UIGradient", main)
grad.Color = ColorSequence.new{ColorSequenceKeypoint.new(0, Color3.fromRGB(45, 45, 60)), ColorSequenceKeypoint.new(1, Color3.fromRGB(20, 20, 30))}
grad.Rotation = 90

-- Dragging support
local dragging = false
local dragStart = nil
local startPos = nil

header.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
		dragStart = input.Position
		startPos = main.Position
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

header.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement then
		input.Changed:Connect(function() end)
	end
end)

game:GetService("UserInputService").InputChanged:Connect(function(input)
	if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		local delta = input.Position - dragStart
		local newPos = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
		main.Position = newPos
	end
end)

-- Minimize / maximize logic
local minimized = false
local normalSize = main.Size
local normalPos = main.Position

local function setMinimized(min)
	if min == minimized then return end
	minimized = min
	if min then
		local tween = TweenService:Create(main, TweenInfo.new(0.25, Enum.EasingStyle.Quad), {Size = UDim2.new(0, 240, 0, 56)})
		tween:Play()
		-- hide content children
		for _, child in ipairs(main:GetChildren()) do
			if child ~= header and child:IsA("Frame") then
				child.Visible = false
			end
		end
		-- change title text a bit
		title.Text = "Yago Menu (min)"
	else
		local tween = TweenService:Create(main, TweenInfo.new(0.25, Enum.EasingStyle.Quad), {Size = normalSize})
		tween:Play()
		for _, child in ipairs(main:GetChildren()) do
			if child ~= header and child:IsA("Frame") then
				child.Visible = true
			end
		end
		title.Text = "Mod Menu"
	end
end

minimizeBtn.MouseButton1Click:Connect(function()
	setMinimized(not minimized)
end)

-- Close button
closeBtn.MouseButton1Click:Connect(function()
	main:Destroy()
end)

-- Small entrance tween
main.Position = UDim2.new(0.5, -210, -0.5, 0)
local entryTween = TweenService:Create(main, TweenInfo.new(0.5, Enum.EasingStyle.Back), {Position = UDim2.new(0.5, -210, 0.2, 0)})
entryTween:Play()

-- End of script
