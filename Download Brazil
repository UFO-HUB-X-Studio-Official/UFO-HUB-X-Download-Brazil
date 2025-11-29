--[[
    UFO HUB X • Tela de download (Brasil 🇧🇷)
    - Fundo: 130548594326307
    - Título "Centro UFO HUB X" aparece letra por letra ~4 segundos
      Regra de cor: "UFO " branco, "HUB X" verde
    - Barra de progresso 0 → 100% em 5 segundos
    - Bandeira 🇧🇷 maior que a barra, grudada na ponta da barra verde
    - Ao terminar, tudo faz fade e some
]]

local Players      = game:GetService("Players")
local CoreGui      = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")

-- remover tela antiga se existir
local OLD = CoreGui:FindFirstChild("UFOX_DownloadScreen")
if OLD then OLD:Destroy() end

local gui = Instance.new("ScreenGui")
gui.Name = "UFOX_DownloadScreen"
gui.IgnoreGuiInset = true
gui.ResetOnSpawn = false
gui.ZIndexBehavior = Enum.ZIndexBehavior.Global
gui.Parent = CoreGui

-- Fundo
local bg = Instance.new("ImageLabel")
bg.Parent = gui
bg.Size = UDim2.fromScale(1,1)
bg.Position = UDim2.fromScale(0.5,0.5)
bg.AnchorPoint = Vector2.new(0.5,0.5)
bg.BackgroundTransparency = 1
bg.Image = "rbxassetid://130548594326307"
bg.ScaleType = Enum.ScaleType.Crop
bg.ImageTransparency = 0

---------------------------------------------------------------------
-- Título "Centro UFO HUB X" (português do Brasil)
-- Regra: "UFO " = branco / "HUB X" = verde
-- Aparece letra por letra em ~4s
---------------------------------------------------------------------
local title = Instance.new("TextLabel")
title.Parent = gui
title.AnchorPoint = Vector2.new(0.5,0.5)
title.Position = UDim2.new(0.5,0,0.32,0)
title.Size = UDim2.new(0.8,0,0,90)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBlack
title.RichText = true
title.TextScaled = true
title.TextColor3 = Color3.new(1,1,1)
title.TextStrokeColor3 = Color3.new(0,0,0)
title.TextStrokeTransparency = 0
title.Text = ""

local fullText = "Centro UFO HUB X"
local totalTime = 4
local steps = #fullText
local stepDelay = totalTime / steps

task.spawn(function()
    for i = 1, steps do
        local text = fullText:sub(1, i)

        -- หา substring "HUB X" แล้วทำส่วนนี้เป็นสีเขียว
        local startIdx, endIdx = string.find(text, "HUB X", 1, true)
        if startIdx then
            local before = text:sub(1, startIdx - 1) -- รวม "Centro UFO "
            local green  = text:sub(startIdx, endIdx) -- "HUB X"
            title.Text = string.format(
                '%s<font color="rgb(25,255,125)">%s</font>',
                before, green
            )
        else
            title.Text = text
        end

        task.wait(stepDelay)
    end
end)

---------------------------------------------------------------------
-- Caixa da barra de download
---------------------------------------------------------------------
local barHolder = Instance.new("Frame")
barHolder.Parent = gui
barHolder.AnchorPoint = Vector2.new(0.5,0.5)
barHolder.Position = UDim2.new(0.5,0,0.55,0)
barHolder.Size = UDim2.new(0.65,0,0,42)
barHolder.BackgroundColor3 = Color3.new(0,0,0)
barHolder.BackgroundTransparency = 0.25
barHolder.ClipsDescendants = false

local corner = Instance.new("UICorner", barHolder)
corner.CornerRadius = UDim.new(0,16)

local stroke = Instance.new("UIStroke", barHolder)
stroke.Thickness = 2
stroke.Color = Color3.new(0,0,0)

-- Barra verde (progresso)
local fill = Instance.new("Frame")
fill.Parent = barHolder
fill.AnchorPoint = Vector2.new(0,0.5)
fill.Position = UDim2.new(0,3,0.5,0)
fill.Size = UDim2.new(0,-6,1,-8) -- começa em 0%
fill.BackgroundColor3 = Color3.fromRGB(25,255,125)
fill.BackgroundTransparency = 0
fill.ClipsDescendants = false

local fillCorner = Instance.new("UICorner", fill)
fillCorner.CornerRadius = UDim.new(0,14)

-- Bandeira do Brasil 🇧🇷 maior que a barra, grudada na ponta
local flag = Instance.new("TextLabel")
flag.Parent = fill
flag.BackgroundTransparency = 1
flag.AnchorPoint = Vector2.new(0.5,0.5)
flag.Position = UDim2.new(1, 24, 0.5, 0)
flag.Size = UDim2.new(0, 70, 0, 70)
flag.Font = Enum.Font.GothamBold
flag.TextScaled = true
flag.Text = "🇧🇷"
flag.ZIndex = 20

-- Texto de download (português)
local label = Instance.new("TextLabel")
label.Parent = barHolder
label.BackgroundTransparency = 1
label.Size = UDim2.new(1,0,1,0)
label.Font = Enum.Font.GothamBold
label.TextColor3 = Color3.new(1,1,1)
label.TextStrokeColor3 = Color3.new(0,0,0)
label.TextStrokeTransparency = 0
label.TextScaled = false
label.TextSize = 20
label.Text = "Baixando 0%"
label.ZIndex = 30

---------------------------------------------------------------------
-- Animação: 0 → 100% e fade out
---------------------------------------------------------------------
local duration = 5
local delayStep = duration / 100

task.spawn(function()
    for i = 0,100 do
        local alpha = i / 100
        fill.Size = UDim2.new(alpha, -6, 1, -8)
        label.Text = ("Baixando %d%%"):format(i)
        task.wait(delayStep)
    end

    local fade = 0.6
    TweenService:Create(bg, TweenInfo.new(fade), {ImageTransparency = 1}):Play()
    TweenService:Create(title, TweenInfo.new(fade), {TextTransparency = 1}):Play()
    TweenService:Create(label, TweenInfo.new(fade), {TextTransparency = 1}):Play()
    TweenService:Create(barHolder, TweenInfo.new(fade), {BackgroundTransparency = 1}):Play()
    TweenService:Create(fill, TweenInfo.new(fade), {BackgroundTransparency = 1}):Play()

    task.wait(fade + 0.2)
    gui:Destroy()
end)
