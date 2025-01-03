-- Script para ativar automaticamente Dragonheart Sword e Dragonstorm Gun
local player = game.Players.LocalPlayer
local mouse = player:GetMouse()

-- Definindo os cooldowns (tempo entre os ataques)
local swordCooldown = 1  -- Intervalo de 1 segundo para a espada
local gunCooldown = 2    -- Intervalo de 2 segundos para a pistola

-- Função de ataque automático com Dragonheart Sword
local function autoDragonheartSword()
	local sword = game.ReplicatedStorage:WaitForChild("DragonheartSword")
	while sword and player.Character:FindFirstChild("HumanoidRootPart") do
		-- Ativa a espada e aguarda o cooldown
		if sword and player.Character:FindFirstChild("HumanoidRootPart") then
			sword:Activate()
			wait(swordCooldown)  -- Aguarda o tempo definido para o próximo ataque
		end
	end
end

-- Função de disparo automático com Dragonstorm Gun
local function autoDragonstormGun()
	local gun = game.ReplicatedStorage:WaitForChild("DragonstormGun")
	while gun and player.Character:FindFirstChild("HumanoidRootPart") do
		-- Ativa a pistola e aguarda o cooldown
		if gun and player.Character:FindFirstChild("HumanoidRootPart") then
			gun:Activate()
			wait(gunCooldown)  -- Aguarda o tempo definido para o próximo disparo
		end
	end
end

-- Função para criar botões na interface
local function createButton(name, position, parent)
	local button = Instance.new("TextButton")
	button.Size = UDim2.new(0, 200, 0, 50)
	button.Position = position
	button.Text = name
	button.BackgroundColor3 = Color3.new(0.2, 0.5, 0.8)
	button.TextColor3 = Color3.new(1, 1, 1)
	button.Parent = parent
	return button
end

-- Lista completa de ilhas por mares
local islands = {
	["Sea 1"] = {
		{Name = "Starter Island", Position = Vector3.new(100, 50, 200)},
		{Name = "Jungle", Position = Vector3.new(-300, 100, 400)},
		{Name = "Pirate Village", Position = Vector3.new(800, 50, -600)},
		{Name = "Desert", Position = Vector3.new(1200, 50, 100)},
		{Name = "Frozen Village", Position = Vector3.new(-600, 100, -900)},
		{Name = "Marine Fortress", Position = Vector3.new(300, 200, -1200)},
		{Name = "Skylands", Position = Vector3.new(0, 500, 0)},
		{Name = "Prison", Position = Vector3.new(1500, 50, -1500)},
		{Name = "Magma Village", Position = Vector3.new(-1000, 50, -500)},
		{Name = "Underwater City", Position = Vector3.new(2000, -50, 800)},
	},
	["Sea 2"] = {
		{Name = "Kingdom of Rose", Position = Vector3.new(-1200, 200, 500)},
		{Name = "Green Zone", Position = Vector3.new(400, 300, 1200)},
		{Name = "Graveyard", Position = Vector3.new(-800, 50, 700)},
		{Name = "Snow Mountain", Position = Vector3.new(1200, 400, -900)},
		{Name = "Hot and Cold", Position = Vector3.new(0, 100, -200)},
		{Name = "Cursed Ship", Position = Vector3.new(-1500, 50, 1500)},
		{Name = "Ice Castle", Position = Vector3.new(1000, 50, -300)},
		{Name = "Forgotten Island", Position = Vector3.new(-2000, 50, 2000)},
	},
	["Sea 3"] = {
		{Name = "Port Town", Position = Vector3.new(3000, 50, -1200)},
		{Name = "Floating Turtle", Position = Vector3.new(-1800, 400, 3000)},
		{Name = "Hydra Island", Position = Vector3.new(500, 50, 2500)},
		{Name = "Great Tree", Position = Vector3.new(-2500, 100, 1500)},
		{Name = "Castle on the Sea", Position = Vector3.new(0, 200, 0)},
		{Name = "Haunted Castle", Position = Vector3.new(-1200, 300, -1800)},
		{Name = "Sea of Treats", Position = Vector3.new(2500, 50, 2500)},
		{Name = "Peanut Island", Position = Vector3.new(-800, 50, 2800)},
		{Name = "Prehistoric Island", Position = Vector3.new(4000, 100, -4000)}, -- Ilha Pré-Histórica
		{Name = "Kitsune Island", Position = Vector3.new(-5000, 150, 5000)},     -- Ilha da Kitsune
		{Name = "Mirage Island", Position = Vector3.new(6000, 100, -6000)},     -- Ilha da Miragem
	}
}

-- Criar interface gráfica
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 400, 0, 600)
frame.Position = UDim2.new(0.5, -200, 0.5, -300)
frame.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
frame.Parent = screenGui

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 50)
title.Text = "Teleport Menu"
title.TextSize = 24
title.TextColor3 = Color3.new(1, 1, 1)
title.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
title.Parent = frame

local yOffset = 60
for sea, seaIslands in pairs(islands) do
	local seaTitle = Instance.new("TextLabel")
	seaTitle.Size = UDim2.new(1, 0, 0, 30)
	seaTitle.Position = UDim2.new(0, 0, 0, yOffset)
	seaTitle.Text = sea
	seaTitle.TextSize = 20
	seaTitle.TextColor3 = Color3.new(1, 1, 1)
	seaTitle.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
	seaTitle.Parent = frame
	yOffset = yOffset + 40

	for _, island in ipairs(seaIslands) do
		local button = createButton(island.Name, UDim2.new(0, 0, 0, yOffset), frame)
		button.MouseButton1Click:Connect(function()
			player.Character.HumanoidRootPart.CFrame = CFrame.new(island.Position)
		end)
		yOffset = yOffset + 60
	end
end

-- Inicia as funções de ataque automático em loop
while true do
	autoDragonheartSword()    -- Chama a função da espada
	autoDragonstormGun()      -- Chama a função da pistola
	wait(1)                   -- Intervalo entre as execuções dos loops
end

-- Script para ativar automaticamente Dragonheart Sword e Dragonstorm Gun
local player = game.Players.LocalPlayer
local mouse = player:GetMouse()

-- Definindo os cooldowns (tempo entre os ataques)
local swordCooldown = 1  -- Intervalo de 1 segundo para a espada
local gunCooldown = 2    -- Intervalo de 2 segundos para a pistola

-- Função de ataque automático com Dragonheart Sword
local function autoDragonheartSword()
	local sword = game.ReplicatedStorage:WaitForChild("DragonheartSword")
	while sword and player.Character:FindFirstChild("HumanoidRootPart") do
		-- Ativa a espada e aguarda o cooldown
		if sword and player.Character:FindFirstChild("HumanoidRootPart") then
			sword:Activate()
			wait(swordCooldown)  -- Aguarda o tempo definido para o próximo ataque
		end
	end
end

-- Função de disparo automático com Dragonstorm Gun
local function autoDragonstormGun()
	local gun = game.ReplicatedStorage:WaitForChild("DragonstormGun")
	while gun and player.Character:FindFirstChild("HumanoidRootPart") do
		-- Ativa a pistola e aguarda o cooldown
		if gun and player.Character:FindFirstChild("HumanoidRootPart") then
			gun:Activate()
			wait(gunCooldown)  -- Aguarda o tempo definido para o próximo disparo
		end
	end
end

-- Função para criar botões na interface
local function createButton(name, position, parent)
	local button = Instance.new("TextButton")
	button.Size = UDim2.new(0, 200, 0, 50)
	button.Position = position
	button.Text = name
	button.BackgroundColor3 = Color3.new(0.2, 0.5, 0.8)
	button.TextColor3 = Color3.new(1, 1, 1)
	button.Parent = parent
	return button
end

-- Lista completa de ilhas por mares
local islands = {
	["Sea 1"] = {
		{Name = "Starter Island", Position = Vector3.new(100, 50, 200)},
		{Name = "Jungle", Position = Vector3.new(-300, 100, 400)},
		{Name = "Pirate Village", Position = Vector3.new(800, 50, -600)},
		{Name = "Desert", Position = Vector3.new(1200, 50, 100)},
		{Name = "Frozen Village", Position = Vector3.new(-600, 100, -900)},
		{Name = "Marine Fortress", Position = Vector3.new(300, 200, -1200)},
		{Name = "Skylands", Position = Vector3.new(0, 500, 0)},
		{Name = "Prison", Position = Vector3.new(1500, 50, -1500)},
		{Name = "Magma Village", Position = Vector3.new(-1000, 50, -500)},
		{Name = "Underwater City", Position = Vector3.new(2000, -50, 800)},
	},
	["Sea 2"] = {
		{Name = "Kingdom of Rose", Position = Vector3.new(-1200, 200, 500)},
		{Name = "Green Zone", Position = Vector3.new(400, 300, 1200)},
		{Name = "Graveyard", Position = Vector3.new(-800, 50, 700)},
		{Name = "Snow Mountain", Position = Vector3.new(1200, 400, -900)},
		{Name = "Hot and Cold", Position = Vector3.new(0, 100, -200)},
		{Name = "Cursed Ship", Position = Vector3.new(-1500, 50, 1500)},
		{Name = "Ice Castle", Position = Vector3.new(1000, 50, -300)},
		{Name = "Forgotten Island", Position = Vector3.new(-2000, 50, 2000)},
	},
	["Sea 3"] = {
		{Name = "Port Town", Position = Vector3.new(3000, 50, -1200)},
		{Name = "Floating Turtle", Position = Vector3.new(-1800, 400, 3000)},
		{Name = "Hydra Island", Position = Vector3.new(500, 50, 2500)},
		{Name = "Great Tree", Position = Vector3.new(-2500, 100, 1500)},
		{Name = "Castle on the Sea", Position = Vector3.new(0, 200, 0)},
		{Name = "Haunted Castle", Position = Vector3.new(-1200, 300, -1800)},
		{Name = "Sea of Treats", Position = Vector3.new(2500, 50, 2500)},
		{Name = "Peanut Island", Position = Vector3.new(-800, 50, 2800)},
		{Name = "Prehistoric Island", Position = Vector3.new(4000, 100, -4000)}, -- Ilha Pré-Histórica
		{Name = "Kitsune Island", Position = Vector3.new(-5000, 150, 5000)},     -- Ilha da Kitsune
		{Name = "Mirage Island", Position = Vector3.new(6000, 100, -6000)},     -- Ilha da Miragem
	}
}

-- Criar interface gráfica
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 400, 0, 600)
frame.Position = UDim2.new(0.5, -200, 0.5, -300)
frame.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
frame.Parent = screenGui

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 50)
title.Text = "Teleport Menu"
title.TextSize = 24
title.TextColor3 = Color3.new(1, 1, 1)
title.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
title.Parent = frame

-- Adicionando ScrollFrame para permitir rolagem
local scrollFrame = Instance.new("ScrollingFrame")
scrollFrame.Size = UDim2.new(1, 0, 1, -50)  -- Ocupa o restante da tela abaixo do título
scrollFrame.Position = UDim2.new(0, 0, 0, 50)
scrollFrame.BackgroundTransparency = 1
scrollFrame.ScrollBarThickness = 10
scrollFrame.Parent = frame

local content = Instance.new("UIListLayout")
content.SortOrder = Enum.SortOrder.LayoutOrder
content.Padding = UDim.new(0, 5)
content.Parent = scrollFrame

local yOffset = 0
for sea, seaIslands in pairs(islands) do
	local seaTitle = Instance.new("TextLabel")
	seaTitle.Size = UDim2.new(1, 0, 0, 30)
	seaTitle.Position = UDim2.new(0, 0, 0, yOffset)
	seaTitle.Text = sea
	seaTitle.TextSize = 20
	seaTitle.TextColor3 = Color3.new(1, 1, 1)
	seaTitle.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
	seaTitle.Parent = scrollFrame
	yOffset = yOffset + 40

	for _, island in ipairs(seaIslands) do
		local button = createButton(island.Name, UDim2.new(0, 0, 0, yOffset), scrollFrame)
		button.MouseButton1Click:Connect(function()
			player.Character.HumanoidRootPart.CFrame = CFrame.new(island.Position)
		end)
		yOffset = yOffset + 60
	end
end

-- Inicia as funções de ataque automático em loop
while true do
	autoDragonheartSword()    -- Chama a função da espada
	autoDragonstormGun()      -- Chama a função da pistola
	wait(1)                   -- Intervalo entre as execuções dos loops
end

local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0, 400, 0, 600)
frame.Position = UDim2.new(0.5, -200, 0.5, -300)
frame.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)

-- Lista das ilhas
local islands = {
	Sea1 = {
		{"Starter Island", Vector3.new(100, 50, 200)},
		{"Jungle", Vector3.new(-300, 100, 400)},
		{"Pirate Village", Vector3.new(800, 50, -600)},
		{"Desert", Vector3.new(1200, 50, 100)},
	},
	Sea2 = {
		{"Kingdom of Rose", Vector3.new(-1200, 200, 500)},
		{"Green Zone", Vector3.new(400, 300, 1200)},
		{"Graveyard", Vector3.new(-800, 50, 700)},
	},
	Sea3 = {
		{"Prehistoric Island", Vector3.new(4000, 100, -4000)},
		{"Kitsune Island", Vector3.new(-5000, 150, 5000)},
		{"Mirage Island", Vector3.new(6000, 100, -6000)},
	},
}

-- Criar o título
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 50)
title.Text = "Teleport Menu"
title.TextSize = 24
title.TextColor3 = Color3.new(1, 1, 1)
title.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)

-- Criar botões dinamicamente
local yOffset = 60
for sea, seaIslands in pairs(islands) do
	local seaTitle = Instance.new("TextLabel", frame)
	seaTitle.Size = UDim2.new(1, 0, 0, 30)
	seaTitle.Position = UDim2.new(0, 0, 0, yOffset)
	seaTitle.Text = sea
	seaTitle.TextSize = 20
	seaTitle.TextColor3 = Color3.new(1, 1, 1)
	seaTitle.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
	yOffset = yOffset + 40

	for _, island in ipairs(seaIslands) do
		local button = Instance.new("TextButton", frame)
		button.Size = UDim2.new(0, 200, 0, 50)
		button.Position = UDim2.new(0, 0, 0, yOffset)
		button.Text = island[1]
		button.BackgroundColor3 = Color3.new(0.2, 0.5, 0.8)
		button.TextColor3 = Color3.new(1, 1, 1)
		button.MouseButton1Click:Connect(function()
			player.Character.HumanoidRootPart.CFrame = CFrame.new(island[2])
		end)
		yOffset = yOffset + 60
	end
end

-- Definir as ilhas e suas posições
local islands = {
	Sea1 = {
		{Name = "Starter Island", Position = Vector3.new(100, 50, 200)},
		{Name = "Jungle", Position = Vector3.new(-300, 100, 400)},
		{Name = "Pirate Village", Position = Vector3.new(800, 50, -600)},
		{Name = "Desert", Position = Vector3.new(1200, 50, 100)},
		{Name = "Frozen Village", Position = Vector3.new(-600, 100, -900)},
		{Name = "Marine Fortress", Position = Vector3.new(300, 200, -1200)},
		{Name = "Skylands", Position = Vector3.new(0, 500, 0)},
		{Name = "Prison", Position = Vector3.new(1500, 50, -1500)},
		{Name = "Magma Village", Position = Vector3.new(-1000, 50, -500)},
		{Name = "Underwater City", Position = Vector3.new(2000, -50, 800)}
	},
	Sea2 = {
		{Name = "Kingdom of Rose", Position = Vector3.new(-1200, 200, 500)},
		{Name = "Green Zone", Position = Vector3.new(400, 300, 1200)},
		{Name = "Graveyard", Position = Vector3.new(-800, 50, 700)},
		{Name = "Snow Mountain", Position = Vector3.new(1200, 400, -900)},
		{Name = "Hot and Cold", Position = Vector3.new(0, 100, -200)},
		{Name = "Cursed Ship", Position = Vector3.new(-1500, 50, 1500)},
		{Name = "Ice Castle", Position = Vector3.new(1000, 50, -300)},
		{Name = "Forgotten Island", Position = Vector3.new(-2000, 50, 2000)}
	},
	Sea3 = {
		{Name = "Port Town", Position = Vector3.new(3000, 50, -1200)},
		{Name = "Floating Turtle", Position = Vector3.new(-1800, 400, 3000)},
		{Name = "Hydra Island", Position = Vector3.new(500, 50, 2500)},
		{Name = "Great Tree", Position = Vector3.new(-2500, 100, 1500)},
		{Name = "Castle on the Sea", Position = Vector3.new(0, 200, 0)},
		{Name = "Haunted Castle", Position = Vector3.new(-1200, 300, -1800)},
		{Name = "Sea of Treats", Position = Vector3.new(2500, 50, 2500)},
		{Name = "Peanut Island", Position = Vector3.new(-800, 50, 2800)},
		{Name = "Prehistoric Island", Position = Vector3.new(4000, 100, -4000)},
		{Name = "Kitsune Island", Position = Vector3.new(-5000, 150, 5000)},
		{Name = "Mirage Island", Position = Vector3.new(6000, 100, -6000)}
	}
}

-- Função para spawnar as ilhas
local function spawnIslands()
	for sea, seaIslands in pairs(islands) do
		for _, island in ipairs(seaIslands) do
			-- Criar a ilha (aqui é apenas um modelo simples, você pode usar um modelo específico de ilha)
			local islandPart = Instance.new("Part")
			islandPart.Size = Vector3.new(100, 10, 100)  -- Tamanho do modelo da ilha
			islandPart.Position = island.Position
			islandPart.Name = island.Name
			islandPart.Anchored = true
			islandPart.Parent = game.Workspace
		end
	end
end

-- Chamar a função para spawnar as ilhas
spawnIslands()

-- Definindo as ilhas e suas posições (continuando do script anterior)
local islands = {
	Sea1 = {
		{Name = "Starter Island", Position = Vector3.new(100, 50, 200)},
		{Name = "Jungle", Position = Vector3.new(-300, 100, 400)},
		{Name = "Pirate Village", Position = Vector3.new(800, 50, -600)},
		{Name = "Desert", Position = Vector3.new(1200, 50, 100)},
	},
	-- Outras Seas...
}

-- Função para criar um botão
local function createButton(name, position, parent, callback)
	local button = Instance.new("TextButton")
	button.Size = UDim2.new(0, 200, 0, 50)
	button.Position = position
	button.Text = name
	button.BackgroundColor3 = Color3.new(0.2, 0.5, 0.8)
	button.TextColor3 = Color3.new(1, 1, 1)
	button.Parent = parent
	button.MouseButton1Click:Connect(callback)
	return button
end

-- Criar interface gráfica
local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 400, 0, 600)
frame.Position = UDim2.new(0.5, -200, 0.5, -300)
frame.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
frame.Parent = screenGui

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 50)
title.Text = "Game Menu"
title.TextSize = 24
title.TextColor3 = Color3.new(1, 1, 1)
title.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
title.Parent = frame

local yOffset = 60

-- Função para criar categorias com seus respectivos botões
local categories = {
	["Farming"] = {
		{Name = "Farm Zone 1", Position = Vector3.new(500, 0, 500)},
		{Name = "Farm Zone 2", Position = Vector3.new(700, 0, 700)}
	},
	["Raids"] = {
		{Name = "Raid 1", Position = Vector3.new(-500, 0, -500)},
		{Name = "Raid 2", Position = Vector3.new(-700, 0, -700)}
	},
	["Fruits"] = {
		{Name = "Fruit Zone 1", Position = Vector3.new(1000, 0, 1000)},
		{Name = "Fruit Zone 2", Position = Vector3.new(1200, 0, 1200)}
	},
	["Teleport"] = {
		{Name = "Sea 1", Position = Vector3.new(2000, 0, 2000)},
		{Name = "Sea 2", Position = Vector3.new(3000, 0, 3000)},
	},
	["Sea Events"] = {
		{Name = "Event 1", Position = Vector3.new(4000, 0, 4000)},
		{Name = "Event 2", Position = Vector3.new(5000, 0, 5000)}
	}
}

-- Criar categorias e botões
for category, items in pairs(categories) do
	-- Categoria como Título
	local categoryTitle = Instance.new("TextLabel")
	categoryTitle.Size = UDim2.new(1, 0, 0, 30)
	categoryTitle.Position = UDim2.new(0, 0, 0, yOffset)
	categoryTitle.Text = category
	categoryTitle.TextSize = 20
	categoryTitle.TextColor3 = Color3.new(1, 1, 1)
	categoryTitle.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
	categoryTitle.Parent = frame
	yOffset = yOffset + 40

	-- Botões de ilhas ou ações dentro da categoria
	for _, island in ipairs(items) do
		local button = createButton(island.Name, UDim2.new(0, 0, 0, yOffset), frame, function()
			player.Character.HumanoidRootPart.CFrame = CFrame.new(island.Position)
		end)
		yOffset = yOffset + 60
	end
end

