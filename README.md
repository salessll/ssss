local Players = game:GetService("Players")
local player = Players.LocalPlayer
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Camera = workspace.CurrentCamera
local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")

-- GUI agora vai para CoreGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "AimbotESPGui"
screenGui.ResetOnSpawn = false
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = CoreGui

local container = Instance.new("Frame")
container.Name = "Container"
container.Size = UDim2.new(0, 480, 0, 360)
container.Position = UDim2.new(0.5, -240, 0.5, -180)
container.BackgroundTransparency = 1
container.Active = true
container.Draggable = true
container.Parent = screenGui

local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 480, 0, 360)
mainFrame.Position = UDim2.new(0, 0, 0, 0)
mainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
mainFrame.BorderSizePixel = 0
mainFrame.Parent = container

local shadow = Instance.new("ImageLabel")
shadow.Name = "Shadow"
shadow.Size = UDim2.new(1, 30, 1, 30)
shadow.Position = UDim2.new(0, -15, 0, -15)
shadow.BackgroundTransparency = 1
shadow.Image = "rbxasset://textures/ui/GuiImagePlaceholder.png"
shadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
shadow.ImageTransparency = 0.5
shadow.ScaleType = Enum.ScaleType.Slice
shadow.SliceCenter = Rect.new(10, 10, 10, 10)
shadow.ZIndex = 0
shadow.Parent = mainFrame

-- ============ PREVIEW FRAME (NOVO) ============
local previewFrame = Instance.new("Frame")
previewFrame.Name = "PreviewFrame"
previewFrame.Size = UDim2.new(0, 200, 0, 360)
previewFrame.Position = UDim2.new(1, 30, 0, 0)
previewFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
previewFrame.BorderSizePixel = 0
previewFrame.Parent = container

local previewShadow = Instance.new("ImageLabel")
previewShadow.Name = "Shadow"
previewShadow.Size = UDim2.new(1, 30, 1, 30)
previewShadow.Position = UDim2.new(0, -15, 0, -15)
previewShadow.BackgroundTransparency = 1
previewShadow.Image = "rbxasset://textures/ui/GuiImagePlaceholder.png"
previewShadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
previewShadow.ImageTransparency = 0.5
previewShadow.ScaleType = Enum.ScaleType.Slice
previewShadow.SliceCenter = Rect.new(10, 10, 10, 10)
previewShadow.ZIndex = 0
previewShadow.Parent = previewFrame

local previewHeader = Instance.new("Frame")
previewHeader.Name = "Header"
previewHeader.Size = UDim2.new(1, 0, 0, 40)
previewHeader.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
previewHeader.BorderSizePixel = 0
previewHeader.Parent = previewFrame

local previewTitle = Instance.new("TextLabel")
previewTitle.Name = "Title"
previewTitle.Size = UDim2.new(1, -20, 1, 0)
previewTitle.Position = UDim2.new(0, 10, 0, 0)
previewTitle.BackgroundTransparency = 1
previewTitle.Text = "◆ PREVIEW"
previewTitle.TextColor3 = Color3.fromRGB(255, 50, 50)
previewTitle.Font = Enum.Font.GothamBold
previewTitle.TextSize = 16
previewTitle.TextXAlignment = Enum.TextXAlignment.Left
previewTitle.Parent = previewHeader

local previewContent = Instance.new("Frame")
previewContent.Name = "Content"
previewContent.Size = UDim2.new(1, 0, 1, -40)
previewContent.Position = UDim2.new(0, 0, 0, 40)
previewContent.BackgroundTransparency = 1
previewContent.Parent = previewFrame
-- BONECO 2D NO PREVIEW
local bonecoContainer = Instance.new("Frame")
bonecoContainer.Name = "BonecoContainer"
bonecoContainer.Size = UDim2.new(0, 100, 0, 200)
bonecoContainer.Position = UDim2.new(0.5, -50, 0.4, -100)
bonecoContainer.BackgroundTransparency = 1
bonecoContainer.Parent = previewContent

local function criarParteBoneco(nome, tamanho, posicao, corPadrao)
    local frame = Instance.new("Frame")
    frame.Name = nome
    frame.Size = tamanho
    frame.Position = posicao
    frame.BackgroundColor3 = corPadrao or Color3.new(1, 1, 1)
    frame.BorderSizePixel = 2
    frame.BorderColor3 = Color3.fromRGB(200, 200, 200)
    frame.Parent = bonecoContainer
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 4)
    corner.Parent = frame
    
    return frame
end

-- Cabeça
local cabecaBoneco = criarParteBoneco("Cabeca", UDim2.new(0, 40, 0, 40), UDim2.new(0.5, -20, 0, 0))

-- Olhos
local olhoEsq = Instance.new("Frame")
olhoEsq.Size = UDim2.new(0, 6, 0, 6)
olhoEsq.Position = UDim2.new(0, 10, 0, 12)
olhoEsq.BackgroundColor3 = Color3.new(0, 0, 0)
olhoEsq.BorderSizePixel = 0
olhoEsq.Parent = cabecaBoneco
local cornerOlhoEsq = Instance.new("UICorner")
cornerOlhoEsq.CornerRadius = UDim.new(1, 0)
cornerOlhoEsq.Parent = olhoEsq

local olhoDir = Instance.new("Frame")
olhoDir.Size = UDim2.new(0, 6, 0, 6)
olhoDir.Position = UDim2.new(0, 24, 0, 12)
olhoDir.BackgroundColor3 = Color3.new(0, 0, 0)
olhoDir.BorderSizePixel = 0
olhoDir.Parent = cabecaBoneco
local cornerOlhoDir = Instance.new("UICorner")
cornerOlhoDir.CornerRadius = UDim.new(1, 0)
cornerOlhoDir.Parent = olhoDir

-- Boca
local boca = Instance.new("Frame")
boca.Size = UDim2.new(0, 14, 0, 2)
boca.Position = UDim2.new(0, 13, 0, 26)
boca.BackgroundColor3 = Color3.new(0, 0, 0)
boca.BorderSizePixel = 0
boca.Parent = cabecaBoneco

-- Torso
local torsoBoneco = criarParteBoneco("Torso", UDim2.new(0, 40, 0, 55), UDim2.new(0.5, -20, 0, 48))

-- Braço Esquerdo
local bracoEsqBoneco = criarParteBoneco("BracoEsq", UDim2.new(0, 10, 0, 48), UDim2.new(0, 10, 0, 52))

-- Braço Direito
local bracoDirBoneco = criarParteBoneco("BracoDir", UDim2.new(0, 10, 0, 48), UDim2.new(1, -20, 0, 52))

-- Perna Esquerda
local pernaEsqBoneco = criarParteBoneco("PernaEsq", UDim2.new(0, 14, 0, 55), UDim2.new(0, 23, 0, 110))

-- Perna Direita
local pernaDirBoneco = criarParteBoneco("PernaDir", UDim2.new(0, 14, 0, 55), UDim2.new(1, -37, 0, 110))
-- ESP PREVIEW ELEMENTS
local espNamePreview = Instance.new("TextLabel")
espNamePreview.Name = "ESPNamePreview"
espNamePreview.Size = UDim2.new(0, 100, 0, 20)
espNamePreview.Position = UDim2.new(0.5, -50, 0, -30)
espNamePreview.BackgroundTransparency = 1
espNamePreview.Text = "Player"
espNamePreview.TextColor3 = Color3.new(1, 1, 1)
espNamePreview.TextStrokeTransparency = 0.5
espNamePreview.Font = Enum.Font.GothamBold
espNamePreview.TextSize = 12
espNamePreview.Visible = false
espNamePreview.Parent = bonecoContainer

local espDistancePreview = Instance.new("TextLabel")
espDistancePreview.Name = "ESPDistancePreview"
espDistancePreview.Size = UDim2.new(0, 100, 0, 18)
espDistancePreview.Position = UDim2.new(0.5, -50, 0, -13)
espDistancePreview.BackgroundTransparency = 1
espDistancePreview.Text = "250m"
espDistancePreview.TextColor3 = Color3.fromRGB(255, 50, 50)
espDistancePreview.TextStrokeTransparency = 0.5
espDistancePreview.Font = Enum.Font.Gotham
espDistancePreview.TextSize = 10
espDistancePreview.Visible = false
espDistancePreview.Parent = bonecoContainer

local espHealthPreview = Instance.new("TextLabel")
espHealthPreview.Name = "ESPHealthPreview"
espHealthPreview.Size = UDim2.new(0, 100, 0, 18)
espHealthPreview.Position = UDim2.new(0.5, -50, 1, 5)
espHealthPreview.BackgroundTransparency = 1
espHealthPreview.Text = "75 HP"
espHealthPreview.TextColor3 = Color3.fromRGB(200, 255, 0)
espHealthPreview.TextStrokeTransparency = 0.5
espHealthPreview.Font = Enum.Font.Gotham
espHealthPreview.TextSize = 10
espHealthPreview.Visible = false
espHealthPreview.Parent = bonecoContainer

local healthBarBgPreview = Instance.new("Frame")
healthBarBgPreview.Name = "HealthBarBg"
healthBarBgPreview.Size = UDim2.new(0.8, 0, 0, 6)
healthBarBgPreview.Position = UDim2.new(0.1, 0, 1, 25)
healthBarBgPreview.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
healthBarBgPreview.BorderSizePixel = 1
healthBarBgPreview.BorderColor3 = Color3.fromRGB(255, 255, 255)
healthBarBgPreview.Visible = false
healthBarBgPreview.Parent = bonecoContainer

local healthBarFillPreview = Instance.new("Frame")
healthBarFillPreview.Name = "Fill"
healthBarFillPreview.Size = UDim2.new(0.75, 0, 1, 0)
healthBarFillPreview.BackgroundColor3 = Color3.fromRGB(200, 255, 0)
healthBarFillPreview.BorderSizePixel = 0
healthBarFillPreview.Parent = healthBarBgPreview

local boxESPPreview = Instance.new("Frame")
boxESPPreview.Name = "BoxESP"
boxESPPreview.Size = UDim2.new(1, 10, 1, 10)
boxESPPreview.Position = UDim2.new(0, -5, 0, -5)
boxESPPreview.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
boxESPPreview.BackgroundTransparency = 1
boxESPPreview.BorderColor3 = Color3.fromRGB(255, 50, 50)
boxESPPreview.BorderSizePixel = 2
boxESPPreview.Visible = false
boxESPPreview.Parent = bonecoContainer

local tracerPreview = Instance.new("Frame")
tracerPreview.Name = "Tracer"
tracerPreview.Size = UDim2.new(0, 2, 0, 80)
tracerPreview.Position = UDim2.new(0.5, -1, 1, 10)
tracerPreview.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
tracerPreview.BorderSizePixel = 0
tracerPreview.Visible = false
tracerPreview.Rotation = 35
tracerPreview.Parent = previewContent

local chamsPreview = Instance.new("Frame")
chamsPreview.Name = "Chams"
chamsPreview.Size = UDim2.new(1, 14, 1, 14)
chamsPreview.Position = UDim2.new(0, -7, 0, -7)
chamsPreview.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
chamsPreview.BackgroundTransparency = 0.7
chamsPreview.BorderSizePixel = 2
chamsPreview.BorderColor3 = Color3.fromRGB(255, 255, 255)
chamsPreview.Visible = false
chamsPreview.ZIndex = 0
chamsPreview.Parent = bonecoContainer

local chamsCorner = Instance.new("UICorner")
chamsCorner.CornerRadius = UDim.new(0, 8)
chamsCorner.Parent = chamsPreview
-- ============ FIM DO PREVIEW, CONTINUAR COM O RESTO ============

local header = Instance.new("Frame")
header.Name = "Header"
header.Size = UDim2.new(1, 0, 0, 40)
header.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
header.BorderSizePixel = 0
header.Parent = mainFrame

local logo = Instance.new("TextLabel")
logo.Name = "Logo"
logo.Size = UDim2.new(0, 150, 1, 0)
logo.Position = UDim2.new(0, 10, 0, 0)
logo.BackgroundTransparency = 1
logo.Text = "◆ AIMBOT"
logo.TextColor3 = Color3.fromRGB(255, 50, 50)
logo.Font = Enum.Font.GothamBold
logo.TextSize = 18
logo.TextXAlignment = Enum.TextXAlignment.Left
logo.Parent = header

local closeBtn = Instance.new("TextButton")
closeBtn.Name = "CloseButton"
closeBtn.Size = UDim2.new(0, 40, 0, 40)
closeBtn.Position = UDim2.new(1, -40, 0, 0)
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
closeBtn.BorderSizePixel = 0
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 16
closeBtn.Parent = header

closeBtn.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

local sideMenu = Instance.new("Frame")
sideMenu.Name = "SideMenu"
sideMenu.Size = UDim2.new(0, 200, 0, 360)
sideMenu.Position = UDim2.new(0, 0, 0, 0)
sideMenu.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
sideMenu.BorderSizePixel = 0
sideMenu.ClipsDescendants = false
sideMenu.Visible = false
sideMenu.Parent = container

local sideShadow = Instance.new("ImageLabel")
sideShadow.Name = "Shadow"
sideShadow.Size = UDim2.new(1, 30, 1, 30)
sideShadow.Position = UDim2.new(0, -15, 0, -15)
sideShadow.BackgroundTransparency = 1
sideShadow.Image = "rbxasset://textures/ui/GuiImagePlaceholder.png"
sideShadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
sideShadow.ImageTransparency = 0.5
sideShadow.ScaleType = Enum.ScaleType.Slice
sideShadow.SliceCenter = Rect.new(10, 10, 10, 10)
sideShadow.ZIndex = 0
sideShadow.Parent = sideMenu

local sideHeader = Instance.new("Frame")
sideHeader.Name = "Header"
sideHeader.Size = UDim2.new(1, 0, 0, 40)
sideHeader.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
sideHeader.BorderSizePixel = 0
sideHeader.Parent = sideMenu

local sideTitle = Instance.new("TextLabel")
sideTitle.Name = "Title"
sideTitle.Size = UDim2.new(1, -20, 1, 0)
sideTitle.Position = UDim2.new(0, 10, 0, 0)
sideTitle.BackgroundTransparency = 1
sideTitle.Text = ""
sideTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
sideTitle.Font = Enum.Font.GothamBold
sideTitle.TextSize = 16
sideTitle.TextXAlignment = Enum.TextXAlignment.Left
sideTitle.Parent = sideHeader

local tabsContainer = Instance.new("Frame")
tabsContainer.Name = "TabsContainer"
tabsContainer.Size = UDim2.new(1, 0, 1, -40)
tabsContainer.Position = UDim2.new(0, 0, 0, 40)
tabsContainer.BackgroundTransparency = 1
tabsContainer.Parent = sideMenu

local tabs = {}
local currentTab = nil
local function createTab(name, yPos)
    local tab = Instance.new("TextButton")
    tab.Name = name .. "Tab"
    tab.Size = UDim2.new(1, -20, 0, 40)
    tab.Position = UDim2.new(0, 10, 0, yPos)
    tab.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    tab.BorderSizePixel = 0
    tab.Text = name
    tab.TextColor3 = Color3.fromRGB(200, 200, 200)
    tab.Font = Enum.Font.GothamBold
    tab.TextSize = 14
    tab.Parent = tabsContainer
    
    tab.MouseEnter:Connect(function()
        if currentTab ~= name then
            tab.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
        end
    end)
    
    tab.MouseLeave:Connect(function()
        if currentTab ~= name then
            tab.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
        end
    end)
    
    tabs[name] = {button = tab, content = nil}
    return tab
end

local function switchTab(tabName)
    for name, tabData in pairs(tabs) do
        if tabData.content then
            tabData.content.Visible = false
            tabData.content.Size = UDim2.new(1, 0, 0, 0)
        end
        tabData.button.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    end
    
    if tabs[tabName] and tabs[tabName].content then
        tabs[tabName].content.Visible = true
        tabs[tabName].button.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
        currentTab = tabName
        logo.Text = "◆ " .. tabName:upper()
        
        local content = tabs[tabName].content
        content.Size = UDim2.new(1, 0, 0, 0)
        local tween = TweenService:Create(content, TweenInfo.new(0.3, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {
            Size = UDim2.new(1, 0, 1, 0)
        })
        tween:Play()
    end
end

local visualTab = createTab("Visuais", 10)
local aimbotTab = createTab("Aimbot", 60)
local playerTab = createTab("Player", 110)
local worldTab = createTab("World", 160)
local configTab = createTab("Config", 210)

visualTab.MouseButton1Click:Connect(function() switchTab("Visuais") end)
aimbotTab.MouseButton1Click:Connect(function() switchTab("Aimbot") end)
playerTab.MouseButton1Click:Connect(function() switchTab("Player") end)
worldTab.MouseButton1Click:Connect(function() switchTab("World") end)
configTab.MouseButton1Click:Connect(function() switchTab("Config") end)

local arrowBtn = Instance.new("TextButton")
arrowBtn.Name = "ArrowButton"
arrowBtn.Size = UDim2.new(0, 20, 0, 50)
arrowBtn.Position = UDim2.new(0, -20, 0.5, -25)
arrowBtn.BackgroundTransparency = 1
arrowBtn.BorderSizePixel = 0
arrowBtn.Text = "◀"
arrowBtn.TextColor3 = Color3.fromRGB(255, 50, 50)
arrowBtn.Font = Enum.Font.GothamBold
arrowBtn.TextSize = 20
arrowBtn.ZIndex = 3
arrowBtn.Parent = mainFrame

local sideMenuOpen = false

arrowBtn.MouseButton1Click:Connect(function()
    sideMenuOpen = not sideMenuOpen
    if sideMenuOpen then
        arrowBtn.Text = "▶"
        sideMenu.Visible = true
        sideMenu.Position = UDim2.new(0, 0, 0, 0)
        arrowBtn:TweenPosition(UDim2.new(0, -290, 0.5, -25), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.3, true)
        sideMenu:TweenPosition(UDim2.new(0, -240, 0, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.3, true)
    else
        arrowBtn.Text = "◀"
        arrowBtn:TweenPosition(UDim2.new(0, -20, 0.5, -25), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.3, true)
        sideMenu:TweenPosition(UDim2.new(0, 0, 0, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.3, true, function()
            sideMenu.Visible = false
        end)
    end
end)

local contentFrame = Instance.new("ScrollingFrame")
contentFrame.Name = "ContentFrame"
contentFrame.Size = UDim2.new(1, -20, 1, -60)
contentFrame.Position = UDim2.new(0, 10, 0, 50)
contentFrame.BackgroundTransparency = 1
contentFrame.BorderSizePixel = 0
contentFrame.ScrollBarThickness = 4
contentFrame.CanvasSize = UDim2.new(0, 0, 0, 1000)
contentFrame.Parent = mainFrame

local aimbotContent = Instance.new("Frame")
aimbotContent.Name = "AimbotContent"
aimbotContent.Size = UDim2.new(1, 0, 1, 0)
aimbotContent.BackgroundTransparency = 1
aimbotContent.Visible = false
aimbotContent.ClipsDescendants = true
aimbotContent.Parent = contentFrame

local visualContent = Instance.new("Frame")
visualContent.Name = "VisualContent"
visualContent.Size = UDim2.new(1, 0, 1, 0)
visualContent.BackgroundTransparency = 1
visualContent.Visible = false
visualContent.ClipsDescendants = true
visualContent.Parent = contentFrame

local playerContent = Instance.new("Frame")
playerContent.Name = "PlayerContent"
playerContent.Size = UDim2.new(1, 0, 1, 0)
playerContent.BackgroundTransparency = 1
playerContent.Visible = false
playerContent.ClipsDescendants = true
playerContent.Parent = contentFrame

local worldContent = Instance.new("Frame")
worldContent.Name = "WorldContent"
worldContent.Size = UDim2.new(1, 0, 1, 0)
worldContent.BackgroundTransparency = 1
worldContent.Visible = false
worldContent.ClipsDescendants = true
worldContent.Parent = contentFrame

local configContent = Instance.new("Frame")
configContent.Name = "ConfigContent"
configContent.Size = UDim2.new(1, 0, 1, 0)
configContent.BackgroundTransparency = 1
configContent.Visible = false
configContent.ClipsDescendants = true
configContent.Parent = contentFrame

tabs["Visuais"].content = visualContent
tabs["Aimbot"].content = aimbotContent
tabs["Player"].content = playerContent
tabs["World"].content = worldContent
tabs["Config"].content = configContent

-- Variáveis Globais
_G.AimbotEnabled = false
_G.ESPEnabled = false
_G.BoxESPEnabled = false
_G.TracersEnabled = false
_G.ChamsEnabled = false
_G.ESPShowName = false
_G.ESPShowDistance = false
_G.ESPShowHealth = false
_G.ESPHealthBar = false
_G.ESPMaxDistance = 20000
_G.BoxESPFilled = false
_G.BoxESPCorner = false
_G.BoxESPThickness = 2
_G.TracerFromBottom = true
_G.TracerTeamCheck = false
_G.TracerThickness = 2
_G.ChamsRainbow = false
_G.ChamsWireframe = false
_G.ChamsTransparency = 0.5
_G.AimbotTargetNPC = false
_G.AimbotWallCheck = false
_G.AimbotSmoothness = 50
_G.AimbotFOVEnabled = false
_G.AimbotFOVSize = 100
_G.AimbotFOVColor = Color3.fromRGB(255, 50, 50)
_G.AimbotBindEnabled = false
_G.AimbotBindKey = nil
_G.AimbotBindKeyName = "None"
_G.MenuBindKey = Enum.KeyCode.Insert
_G.MenuBindKeyName = "Insert"
_G.MenuTransparency = 0
_G.ShadowIntensity = 50
_G.FriendsList = {}
_G.AimbotTargetPart = "Head"

local espObjects = {}
local boxESPObjects = {}
local tracerObjects = {}
local chamsObjects = {}
local fovCircle = nil
local aimbotActive = false
local lockedTarget = nil

pcall(function()
    fovCircle = Drawing.new("Circle")
    fovCircle.Visible = false
    fovCircle.Thickness = 2
    fovCircle.Color = Color3.fromRGB(255, 50, 50)
    fovCircle.NumSides = 64
    fovCircle.Radius = 100
    fovCircle.Transparency = 1
    fovCircle.Filled = false
end)
local function createSection(name, yPos)
    local section = Instance.new("Frame")
    section.Name = name .. "Section"
    section.Size = UDim2.new(0, 210, 0, 180)
    section.Position = UDim2.new(0, (yPos % 2) * 230, 0, math.floor(yPos / 2) * 190)
    section.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    section.BorderSizePixel = 0
    section.Parent = contentFrame
    
    local title = Instance.new("TextLabel")
    title.Name = "Title"
    title.Size = UDim2.new(1, -40, 0, 30)
    title.Position = UDim2.new(0, 10, 0, 5)
    title.BackgroundTransparency = 1
    title.Text = name
    title.TextColor3 = Color3.fromRGB(255, 255, 255)
    title.Font = Enum.Font.GothamBold
    title.TextSize = 14
    title.TextXAlignment = Enum.TextXAlignment.Left
    title.Parent = section
    
    local toggleBtn = Instance.new("TextButton")
    toggleBtn.Name = "Toggle"
    toggleBtn.Size = UDim2.new(0, 40, 0, 20)
    toggleBtn.Position = UDim2.new(1, -45, 0, 10)
    toggleBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    toggleBtn.BorderSizePixel = 0
    toggleBtn.Text = ""
    toggleBtn.Parent = section
    
    local toggleIndicator = Instance.new("Frame")
    toggleIndicator.Name = "Indicator"
    toggleIndicator.Size = UDim2.new(0, 16, 0, 16)
    toggleIndicator.Position = UDim2.new(0, 2, 0, 2)
    toggleIndicator.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
    toggleIndicator.BorderSizePixel = 0
    toggleIndicator.Parent = toggleBtn
    
    return section, toggleBtn, toggleIndicator
end

local function createOption(parent, name, yPos, callback)
    local option = Instance.new("Frame")
    option.Name = name
    option.Size = UDim2.new(1, -20, 0, 25)
    option.Position = UDim2.new(0, 10, 0, yPos)
    option.BackgroundTransparency = 1
    option.Parent = parent
    
    local checkbox = Instance.new("TextButton")
    checkbox.Name = "Checkbox"
    checkbox.Size = UDim2.new(0, 16, 0, 16)
    checkbox.Position = UDim2.new(0, 0, 0, 4)
    checkbox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    checkbox.BorderColor3 = Color3.fromRGB(255, 50, 50)
    checkbox.BorderSizePixel = 1
    checkbox.Text = ""
    checkbox.Parent = option
    
    local checkmark = Instance.new("TextLabel")
    checkmark.Size = UDim2.new(1, 0, 1, 0)
    checkmark.BackgroundTransparency = 1
    checkmark.Text = "✓"
    checkmark.TextColor3 = Color3.fromRGB(255, 50, 50)
    checkmark.Font = Enum.Font.GothamBold
    checkmark.TextSize = 14
    checkmark.Visible = false
    checkmark.Parent = checkbox
    
    local label = Instance.new("TextLabel")
    label.Name = "Label"
    label.Size = UDim2.new(1, -25, 1, 0)
    label.Position = UDim2.new(0, 25, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = name
    label.TextColor3 = Color3.fromRGB(200, 200, 200)
    label.Font = Enum.Font.Gotham
    label.TextSize = 12
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = option
    
    checkbox.MouseButton1Click:Connect(function()
        checkmark.Visible = not checkmark.Visible
        if callback then callback(checkmark.Visible) end
    end)
    
    return option, checkbox, checkmark
end

local function createSlider(parent, name, yPos, min, max, default, callback)
    local sliderFrame = Instance.new("Frame")
    sliderFrame.Name = name
    sliderFrame.Size = UDim2.new(1, -20, 0, 40)
    sliderFrame.Position = UDim2.new(0, 10, 0, yPos)
    sliderFrame.BackgroundTransparency = 1
    sliderFrame.Parent = parent
    
    local value = default
    
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, -40, 0, 15)
    label.BackgroundTransparency = 1
    label.Text = name
    label.TextColor3 = Color3.fromRGB(200, 200, 200)
    label.Font = Enum.Font.Gotham
    label.TextSize = 11
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = sliderFrame
    
    local valueLabel = Instance.new("TextLabel")
    valueLabel.Size = UDim2.new(0, 35, 0, 15)
    valueLabel.Position = UDim2.new(1, -35, 0, 0)
    valueLabel.BackgroundTransparency = 1
    valueLabel.Text = tostring(default)
    valueLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
    valueLabel.Font = Enum.Font.GothamBold
    valueLabel.TextSize = 11
    valueLabel.TextXAlignment = Enum.TextXAlignment.Right
    valueLabel.Parent = sliderFrame
    
    local sliderBg = Instance.new("Frame")
    sliderBg.Name = "SliderBg"
    sliderBg.Size = UDim2.new(1, 0, 0, 6)
    sliderBg.Position = UDim2.new(0, 0, 0, 20)
    sliderBg.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    sliderBg.BorderSizePixel = 0
    sliderBg.Parent = sliderFrame
    
    local sliderFill = Instance.new("Frame")
    sliderFill.Name = "Fill"
    sliderFill.Size = UDim2.new((default - min) / (max - min), 0, 1, 0)
    sliderFill.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    sliderFill.BorderSizePixel = 0
    sliderFill.Parent = sliderBg
    
    local dragging = false
    
    local function updateSlider(input)
        local relativeX = math.clamp((input.Position.X - sliderBg.AbsolutePosition.X) / sliderBg.AbsoluteSize.X, 0, 1)
        value = math.floor(min + (max - min) * relativeX)
        sliderFill.Size = UDim2.new(relativeX, 0, 1, 0)
        valueLabel.Text = tostring(value)
        if callback then callback(value) end
    end
    
    sliderBg.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            updateSlider(input)
        end
    end)
    
    sliderBg.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = false
        end
    end)
    
    UserInputService.InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
            updateSlider(input)
        end
    end)
    
    return sliderFrame
end

local function createBindButton(parent, name, yPos, callback)
    local bindFrame = Instance.new("Frame")
    bindFrame.Name = name
    bindFrame.Size = UDim2.new(1, -20, 0, 30)
    bindFrame.Position = UDim2.new(0, 10, 0, yPos)
    bindFrame.BackgroundTransparency = 1
    bindFrame.Parent = parent
    
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(0.5, 0, 1, 0)
    label.BackgroundTransparency = 1
    label.Text = name
    label.TextColor3 = Color3.fromRGB(200, 200, 200)
    label.Font = Enum.Font.Gotham
    label.TextSize = 12
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = bindFrame
    
    local bindBtn = Instance.new("TextButton")
    bindBtn.Size = UDim2.new(0.5, -5, 0, 25)
    bindBtn.Position = UDim2.new(0.5, 0, 0, 2)
    bindBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    bindBtn.BorderSizePixel = 0
    bindBtn.Text = "None"
    bindBtn.TextColor3 = Color3.fromRGB(200, 200, 200)
    bindBtn.Font = Enum.Font.Gotham
    bindBtn.TextSize = 11
    bindBtn.Parent = bindFrame
    
    local binding = false
    
    bindBtn.MouseButton1Click:Connect(function()
        if binding then return end
        binding = true
        bindBtn.Text = "..."
        bindBtn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    end)
    
    UserInputService.InputBegan:Connect(function(input)
        if not binding then return end
        local keyName = ""
        local keyValue = nil
        
        if input.UserInputType == Enum.UserInputType.Keyboard then
            keyName = input.KeyCode.Name
            keyValue = input.KeyCode
        elseif input.UserInputType == Enum.UserInputType.MouseButton1 then
            keyName = "LMB"
            keyValue = Enum.UserInputType.MouseButton1
        elseif input.UserInputType == Enum.UserInputType.MouseButton2 then
            keyName = "RMB"
            keyValue = Enum.UserInputType.MouseButton2
        elseif input.UserInputType == Enum.UserInputType.MouseButton3 then
            keyName = "MMB"
            keyValue = Enum.UserInputType.MouseButton3
        end
        
        if keyName ~= "" then
            bindBtn.Text = keyName
            bindBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            binding = false
            if callback then callback(keyValue, keyName) end
        end
    end)
    
    return bindFrame, bindBtn
end

local function createFriendsSelector(parent, yPos)
    local friendsFrame = Instance.new("ScrollingFrame")
    friendsFrame.Name = "FriendsSelector"
    friendsFrame.Size = UDim2.new(1, -20, 0, 130)
    friendsFrame.Position = UDim2.new(0, 10, 0, yPos)
    friendsFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    friendsFrame.BorderSizePixel = 0
    friendsFrame.ScrollBarThickness = 4
    friendsFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
    friendsFrame.Parent = parent
    
    local function updatePlayerList()
        for _, child in pairs(friendsFrame:GetChildren()) do
            if child:IsA("Frame") then
                child:Destroy()
            end
        end
        
        local yOffset = 0
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= player then
                local playerFrame = Instance.new("Frame")
                playerFrame.Name = p.Name
                playerFrame.Size = UDim2.new(1, -10, 0, 25)
                playerFrame.Position = UDim2.new(0, 5, 0, yOffset)
                playerFrame.BackgroundTransparency = 1
                playerFrame.Parent = friendsFrame
                
                local checkbox = Instance.new("TextButton")
                checkbox.Size = UDim2.new(0, 16, 0, 16)
                checkbox.Position = UDim2.new(0, 0, 0, 4)
                checkbox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
                checkbox.BorderColor3 = Color3.fromRGB(255, 50, 50)
                checkbox.BorderSizePixel = 1
                checkbox.Text = ""
                checkbox.Parent = playerFrame
                
                local checkmark = Instance.new("TextLabel")
                checkmark.Size = UDim2.new(1, 0, 1, 0)
                checkmark.BackgroundTransparency = 1
                checkmark.Text = "✓"
                checkmark.TextColor3 = Color3.fromRGB(255, 50, 50)
                checkmark.Font = Enum.Font.GothamBold
                checkmark.TextSize = 14
                checkmark.Visible = table.find(_G.FriendsList, p.Name) ~= nil
                checkmark.Parent = checkbox
                
                local nameLabel = Instance.new("TextLabel")
                nameLabel.Size = UDim2.new(1, -25, 1, 0)
                nameLabel.Position = UDim2.new(0, 25, 0, 0)
                nameLabel.BackgroundTransparency = 1
                nameLabel.Text = p.Name
                nameLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
                nameLabel.Font = Enum.Font.Gotham
                nameLabel.TextSize = 12
                nameLabel.TextXAlignment = Enum.TextXAlignment.Left
                nameLabel.Parent = playerFrame
                
                checkbox.MouseButton1Click:Connect(function()
                    checkmark.Visible = not checkmark.Visible
                    if checkmark.Visible then
                        table.insert(_G.FriendsList, p.Name)
                    else
                        local index = table.find(_G.FriendsList, p.Name)
                        if index then
                            table.remove(_G.FriendsList, index)
                        end
                    end
                end)
                
                yOffset = yOffset + 30
            end
        end
        
        friendsFrame.CanvasSize = UDim2.new(0, 0, 0, yOffset)
    end
    
    updatePlayerList()
    Players.PlayerAdded:Connect(updatePlayerList)
    Players.PlayerRemoving:Connect(updatePlayerList)
    
    return friendsFrame
end

local function getAllTargets()
    local targets = {}
    for _, p in pairs(Players:GetPlayers()) do
        if p ~= player and p.Character then
            table.insert(targets, {character = p.Character, player = p})
        end
    end
    
    if _G.AimbotTargetNPC then
        for _, v in pairs(workspace:GetDescendants()) do
            if v:IsA("Model") and v:FindFirstChild("Humanoid") and v:FindFirstChild("Head") and not Players:GetPlayerFromCharacter(v) then
                table.insert(targets, {character = v, player = nil})
            end
        end
    end
    
    return targets
end

local function createESP(p)
    pcall(function()
        if not p or not p.Character then return end
        
        if espObjects[p] and espObjects[p].billboard then
            espObjects[p].billboard:Destroy()
        end
        
        local hrp = p.Character:FindFirstChild("HumanoidRootPart")
        if not hrp then return end
        
        local billboard = Instance.new("BillboardGui")
        billboard.Name = "ESP_Billboard"
        billboard.Adornee = hrp
        billboard.Size = UDim2.new(0, 200, 0, 100)
        billboard.StudsOffset = Vector3.new(0, 3, 0)
        billboard.AlwaysOnTop = true
        billboard.Parent = hrp
        
        local nameLabel = Instance.new("TextLabel")
        nameLabel.Size = UDim2.new(1, 0, 0.25, 0)
        nameLabel.BackgroundTransparency = 1
        nameLabel.Text = p.Name
        nameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        nameLabel.TextStrokeTransparency = 0.5
        nameLabel.Font = Enum.Font.GothamBold
        nameLabel.TextSize = 14
        nameLabel.Visible = _G.ESPShowName
        nameLabel.Parent = billboard
        
        local distanceLabel = Instance.new("TextLabel")
        distanceLabel.Size = UDim2.new(1, 0, 0.25, 0)
        distanceLabel.Position = UDim2.new(0, 0, 0.25, 0)
        distanceLabel.BackgroundTransparency = 1
        distanceLabel.Text = "0m"
        distanceLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
        distanceLabel.TextStrokeTransparency = 0.5
        distanceLabel.Font = Enum.Font.Gotham
        distanceLabel.TextSize = 12
        distanceLabel.Visible = _G.ESPShowDistance
        distanceLabel.Parent = billboard
        
        local healthLabel = Instance.new("TextLabel")
        healthLabel.Size = UDim2.new(1, 0, 0.25, 0)
        healthLabel.Position = UDim2.new(0, 0, 0.5, 0)
        healthLabel.BackgroundTransparency = 1
        healthLabel.Text = "100 HP"
        healthLabel.TextColor3 = Color3.fromRGB(0, 255, 0)
        healthLabel.TextStrokeTransparency = 0.5
        healthLabel.Font = Enum.Font.Gotham
        healthLabel.TextSize = 12
        healthLabel.Visible = _G.ESPShowHealth
        healthLabel.Parent = billboard
        
        local healthBarBg = Instance.new("Frame")
        healthBarBg.Name = "HealthBarBg"
        healthBarBg.Size = UDim2.new(0.8, 0, 0.08, 0)
        healthBarBg.Position = UDim2.new(0.1, 0, 0.75, 0)
        healthBarBg.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
        healthBarBg.BorderSizePixel = 1
        healthBarBg.BorderColor3 = Color3.fromRGB(255, 255, 255)
        healthBarBg.Visible = _G.ESPHealthBar
        healthBarBg.Parent = billboard
        
        local healthBarFill = Instance.new("Frame")
        healthBarFill.Name = "HealthBarFill"
        healthBarFill.Size = UDim2.new(1, 0, 1, 0)
        healthBarFill.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
        healthBarFill.BorderSizePixel = 0
        healthBarFill.Parent = healthBarBg
        
        espObjects[p] = {
            billboard = billboard, 
            nameLabel = nameLabel, 
            distanceLabel = distanceLabel, 
            healthLabel = healthLabel,
            healthBarBg = healthBarBg,
            healthBarFill = healthBarFill
        }
    end)
end

local function createBoxESP(p)
    pcall(function()
        if not p or not p.Character then return end
        
        if boxESPObjects[p] and boxESPObjects[p].container then
            boxESPObjects[p].container:Destroy()
        end
        
        local hrp = p.Character:FindFirstChild("HumanoidRootPart")
        if not hrp then return end
        
        local boxContainer = Instance.new("BillboardGui")
        boxContainer.Name = "BoxESP"
        boxContainer.Adornee = hrp
        boxContainer.Size = UDim2.new(4, 0, 5, 0)
        boxContainer.AlwaysOnTop = true
        boxContainer.Parent = hrp
        
        local box = Instance.new("Frame")
        box.Size = UDim2.new(1, 0, 1, 0)
        box.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
        box.BackgroundTransparency = _G.BoxESPFilled and 0.7 or 1
        box.BorderColor3 = Color3.fromRGB(255, 50, 50)
        box.BorderSizePixel = _G.BoxESPThickness
        box.Parent = boxContainer
        
        if _G.BoxESPCorner then
            for i = 1, 4 do
                local corner = Instance.new("Frame")
                corner.Size = UDim2.new(0.2, 0, 0.1, 0)
                corner.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
                corner.BorderSizePixel = 0
                if i == 1 then corner.Position = UDim2.new(0, 0, 0, 0)
                elseif i == 2 then corner.Position = UDim2.new(0.8, 0, 0, 0)
                elseif i == 3 then corner.Position = UDim2.new(0, 0, 0.9, 0)
                else corner.Position = UDim2.new(0.8, 0, 0.9, 0) end
                corner.Parent = box
            end
        end
        
        boxESPObjects[p] = {container = boxContainer, box = box}
    end)
end

local function createTracerLine(p)
    pcall(function()
        if not p or not p.Character then return end
        
        if tracerObjects[p] then
            tracerObjects[p]:Remove()
        end
        
        local line = Drawing.new("Line")
        line.Visible = false
        line.Color = Color3.fromRGB(255, 50, 50)
        line.Thickness = _G.TracerThickness
        line.Transparency = 1
        tracerObjects[p] = line
    end)
end

local function createChams(p)
    pcall(function()
        if not p or not p.Character then return end
        
        if chamsObjects[p] then
            chamsObjects[p]:Destroy()
        end
        
        local highlight = Instance.new("Highlight")
        highlight.Name = "Chams"
        highlight.Adornee = p.Character
        highlight.FillColor = Color3.fromRGB(255, 50, 50)
        highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
        highlight.FillTransparency = _G.ChamsTransparency
        highlight.OutlineTransparency = 0
        highlight.Parent = p.Character
        
        chamsObjects[p] = highlight
    end)
end

local function removeESP(p)
    if espObjects[p] then
        if espObjects[p].billboard then pcall(function() espObjects[p].billboard:Destroy() end) end
        espObjects[p] = nil
    end
end

local function removeBoxESP(p)
    if boxESPObjects[p] then
        if boxESPObjects[p].container then pcall(function() boxESPObjects[p].container:Destroy() end) end
        boxESPObjects[p] = nil
    end
end

local function removeTracer(p)
    if tracerObjects[p] then
        pcall(function() tracerObjects[p]:Remove() end)
        tracerObjects[p] = nil
    end
end

local function removeChams(p)
    if chamsObjects[p] then
        pcall(function() chamsObjects[p]:Destroy() end)
        chamsObjects[p] = nil
    end
end

local function toggleESP(enabled)
    if enabled then
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= player then 
                task.spawn(function() createESP(p) end)
            end
        end
    else
        for p, _ in pairs(espObjects) do removeESP(p) end
    end
end

local function toggleBoxESP(enabled)
    if enabled then
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= player then 
                task.spawn(function() createBoxESP(p) end)
            end
        end
    else
        for p, _ in pairs(boxESPObjects) do removeBoxESP(p) end
    end
end

local function toggleTracers(enabled)
    if enabled then
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= player then 
                task.spawn(function() createTracerLine(p) end)
            end
        end
    else
        for p, _ in pairs(tracerObjects) do removeTracer(p) end
    end
end

local function toggleChams(enabled)
    if enabled then
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= player then 
                task.spawn(function() createChams(p) end)
            end
        end
    else
        for p, _ in pairs(chamsObjects) do removeChams(p) end
    end
end

local function isVisible(char)
    if not _G.AimbotWallCheck then return true end
    if not player.Character or not player.Character:FindFirstChild("Head") then return false end
    
    local origin = player.Character.Head.Position
    local target = char:FindFirstChild("Head")
    if not target then return false end
    
    local ray = Ray.new(origin, (target.Position - origin).Unit * 1000)
    local hit = workspace:FindPartOnRayWithIgnoreList(ray, {player.Character, char})
    return hit == nil or hit:IsDescendantOf(char)
end

local function isFriend(targetPlayer)
    if not targetPlayer then return false end
    return table.find(_G.FriendsList, targetPlayer.Name) ~= nil
end

local function getClosestTarget()
    local closest = nil
    local shortestDist = math.huge
    local mousePos = UserInputService:GetMouseLocation()
    local targets = getAllTargets()
    
    for _, targetData in pairs(targets) do
        local char = targetData.character
        local targetPlayer = targetData.player
        
        if isFriend(targetPlayer) then continue end
        
        local targetPart
        if _G.AimbotTargetPart == "Head" then
            targetPart = char:FindFirstChild("Head")
        else
            targetPart = char:FindFirstChild("HumanoidRootPart") or char:FindFirstChild("Torso")
        end
        
        local hum = char:FindFirstChild("Humanoid")
        
        if targetPart and hum and hum.Health > 0 and isVisible(char) then
            local screenPos, onScreen = Camera:WorldToScreenPoint(targetPart.Position)
            
            if onScreen then
                local distance = (Vector2.new(screenPos.X, screenPos.Y) - mousePos).Magnitude
                
                if _G.AimbotFOVEnabled then
                    if distance <= _G.AimbotFOVSize and distance < shortestDist then
                        closest = targetPart
                        shortestDist = distance
                    end
                else
                    if distance < shortestDist then
                        closest = targetPart
                        shortestDist = distance
                    end
                end
            end
        end
    end
    
    return closest
end

-- SEÇÃO AIMBOT MODIFICADA
local aimbotSec, aimbotToggle, aimbotInd = createSection("Aimbot", 0)
aimbotSec.Parent = aimbotContent
aimbotSec.Size = UDim2.new(0, 210, 0, 230)

-- DROPDOWN TARGET PART
local targetPartFrame = Instance.new("Frame")
targetPartFrame.Name = "TargetPart"
targetPartFrame.Size = UDim2.new(1, -20, 0, 30)
targetPartFrame.Position = UDim2.new(0, 10, 0, 40)
targetPartFrame.BackgroundTransparency = 1
targetPartFrame.Parent = aimbotSec

local targetLabel = Instance.new("TextLabel")
targetLabel.Size = UDim2.new(0.5, 0, 1, 0)
targetLabel.BackgroundTransparency = 1
targetLabel.Text = "Target Part"
targetLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
targetLabel.Font = Enum.Font.Gotham
targetLabel.TextSize = 12
targetLabel.TextXAlignment = Enum.TextXAlignment.Left
targetLabel.Parent = targetPartFrame

local targetDropdown = Instance.new("TextButton")
targetDropdown.Name = "Dropdown"
targetDropdown.Size = UDim2.new(0.5, -5, 0, 25)
targetDropdown.Position = UDim2.new(0.5, 0, 0, 2)
targetDropdown.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
targetDropdown.BorderSizePixel = 0
targetDropdown.Text = "Head"
targetDropdown.TextColor3 = Color3.fromRGB(200, 200, 200)
targetDropdown.Font = Enum.Font.Gotham
targetDropdown.TextSize = 11
targetDropdown.Parent = targetPartFrame

local dropdownOpen = false
local dropdownOptions = Instance.new("Frame")
dropdownOptions.Name = "Options"
dropdownOptions.Size = UDim2.new(0.5, -5, 0, 50)
dropdownOptions.Position = UDim2.new(0.5, 0, 0, 27)
dropdownOptions.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
dropdownOptions.BorderSizePixel = 0
dropdownOptions.Visible = false
dropdownOptions.ZIndex = 10
dropdownOptions.Parent = targetPartFrame

local headOption = Instance.new("TextButton")
headOption.Size = UDim2.new(1, 0, 0, 25)
headOption.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
headOption.BorderSizePixel = 0
headOption.Text = "Head"
headOption.TextColor3 = Color3.fromRGB(200, 200, 200)
headOption.Font = Enum.Font.Gotham
headOption.TextSize = 11
headOption.Parent = dropdownOptions
local humanoidOption = Instance.new("TextButton")
humanoidOption.Size = UDim2.new(1, 0, 0, 25)
humanoidOption.Position = UDim2.new(0, 0, 0, 25)
humanoidOption.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
humanoidOption.BorderSizePixel = 0
humanoidOption.Text = "Humanoid"
humanoidOption.TextColor3 = Color3.fromRGB(200, 200, 200)
humanoidOption.Font = Enum.Font.Gotham
humanoidOption.TextSize = 11
humanoidOption.Parent = dropdownOptions
targetDropdown.MouseButton1Click:Connect(function()
dropdownOpen = not dropdownOpen
dropdownOptions.Visible = dropdownOpen
end)
headOption.MouseButton1Click:Connect(function()
_G.AimbotTargetPart = "Head"
targetDropdown.Text = "Head"
dropdownOptions.Visible = false
dropdownOpen = false
cabecaBoneco.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
torsoBoneco.BackgroundColor3 = Color3.new(1, 1, 1)
end)
humanoidOption.MouseButton1Click:Connect(function()
_G.AimbotTargetPart = "Humanoid"
targetDropdown.Text = "Humanoid"
dropdownOptions.Visible = false
dropdownOpen = false
cabecaBoneco.BackgroundColor3 = Color3.new(1, 1, 1)
torsoBoneco.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
end)
createOption(aimbotSec, "Target NPC", 75, function(e) _G.AimbotTargetNPC = e end)
createOption(aimbotSec, "Wall Check", 100, function(e) _G.AimbotWallCheck = e end)
createSlider(aimbotSec, "Smoothness", 130, 1, 100, 50, function(v) _G.AimbotSmoothness = v end)
createBindButton(aimbotSec, "Keybind", 175, function(key, name)
_G.AimbotBindKey = key
_G.AimbotBindKeyName = name
_G.AimbotBindEnabled = (name ~= "None")
end)
local friendsSec, friendsToggle, friendsInd = createSection("Friends", 1)
friendsSec.Parent = aimbotContent
friendsSec.Size = UDim2.new(0, 210, 0, 180)
createFriendsSelector(friendsSec, 40)
-- SEÇÕES ESP COM PREVIEW
local espSec, espToggle, espInd = createSection("ESP", 0)
espSec.Parent = visualContent
createOption(espSec, "Show Name", 40, function(e)
_G.ESPShowName = e
espNamePreview.Visible = e
for _, d in pairs(espObjects) do
if d.nameLabel then d.nameLabel.Visible = e end
end
end)
createOption(espSec, "Show Distance", 65, function(e)
_G.ESPShowDistance = e
espDistancePreview.Visible = e
for _, d in pairs(espObjects) do
if d.distanceLabel then d.distanceLabel.Visible = e end
end
end)
createOption(espSec, "Show Health", 90, function(e)
_G.ESPShowHealth = e
espHealthPreview.Visible = e
for _, d in pairs(espObjects) do
if d.healthLabel then d.healthLabel.Visible = e end
end
end)
createOption(espSec, "Health Bar", 115, function(e)
_G.ESPHealthBar = e
healthBarBgPreview.Visible = e
for _, d in pairs(espObjects) do
if d.healthBarBg then d.healthBarBg.Visible = e end
end
end)
createSlider(espSec, "Max Distance", 145, 100, 20000, 20000, function(v) _G.ESPMaxDistance = v end)
local boxSec, boxToggle, boxInd = createSection("Box ESP", 1)
boxSec.Parent = visualContent
createOption(boxSec, "Filled Boxes", 40, function(e)
_G.BoxESPFilled = e
boxESPPreview.BackgroundTransparency = e and 0.7 or 1
for _, d in pairs(boxESPObjects) do
if d.box then d.box.BackgroundTransparency = e and 0.7 or 1 end
end
end)
createOption(boxSec, "Corner Boxes", 65, function(e)
_G.BoxESPCorner = e
toggleBoxESP(false)
task.wait(0.1)
toggleBoxESP(_G.BoxESPEnabled)
end)
createSlider(boxSec, "Thickness", 95, 1, 5, 2, function(v)
_G.BoxESPThickness = v
boxESPPreview.BorderSizePixel = v
for _, d in pairs(boxESPObjects) do
if d.box then d.box.BorderSizePixel = v end
end
end)
local tracerSec, tracerToggle, tracerInd = createSection("Tracers", 2)
tracerSec.Parent = visualContent
createOption(tracerSec, "From Bottom", 40, function(e) _G.TracerFromBottom = e end)
createOption(tracerSec, "Team Check", 65, function(e) _G.TracerTeamCheck = e end)
createSlider(tracerSec, "Thickness", 95, 1, 5, 2, function(v)
_G.TracerThickness = v
tracerPreview.Size = UDim2.new(0, v, 0, 80)
for _, t in pairs(tracerObjects) do t.Thickness = v end
end)
local chamSec, chamToggle, chamInd = createSection("Chams", 3)
chamSec.Parent = visualContent
createOption(chamSec, "Rainbow Chams", 40, function(e) _G.ChamsRainbow = e end)
createOption(chamSec, "Wireframe", 65, function(e) _G.ChamsWireframe = e end)
createSlider(chamSec, "Transparency", 95, 0, 100, 50, function(v)
_G.ChamsTransparency = v / 100
chamsPreview.BackgroundTransparency = v / 100
for _, h in pairs(chamsObjects) do h.FillTransparency = v / 100 end
end)
local configSec, configToggle, configInd = createSection("Settings", 0)
configSec.Parent = configContent
configSec.Size = UDim2.new(0, 210, 0, 140)
createBindButton(configSec, "Menu Bind", 40, function(key, name)
_G.MenuBindKey = key
_G.MenuBindKeyName = name
end)
createSlider(configSec, "Transparency", 75, 0, 100, 0, function(v)
_G.MenuTransparency = v / 100
mainFrame.BackgroundTransparency = v / 100
sideMenu.BackgroundTransparency = v / 100
header.BackgroundTransparency = v / 100
sideHeader.BackgroundTransparency = v / 100
previewFrame.BackgroundTransparency = v / 100
previewHeader.BackgroundTransparency = v / 100
end)
createSlider(configSec, "Shadow Intensity", 120, 0, 100, 50, function(v)
_G.ShadowIntensity = v
shadow.ImageTransparency = 1 - (v / 100)
sideShadow.ImageTransparency = 1 - (v / 100)
previewShadow.ImageTransparency = 1 - (v / 100)
end)
-- TOGGLE CONNECTIONS
aimbotToggle.MouseButton1Click:Connect(function()
_G.AimbotEnabled = not _G.AimbotEnabled
aimbotToggle.BackgroundColor3 = _G.AimbotEnabled and Color3.fromRGB(255, 50, 50) or Color3.fromRGB(60, 60, 60)
aimbotInd.BackgroundColor3 = _G.AimbotEnabled and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(100, 100, 100)
aimbotInd.Position = _G.AimbotEnabled and UDim2.new(1, -18, 0, 2) or UDim2.new(0, 2, 0, 2)
end)
espToggle.MouseButton1Click:Connect(function()
_G.ESPEnabled = not _G.ESPEnabled
espToggle.BackgroundColor3 = _G.ESPEnabled and Color3.fromRGB(255, 50, 50) or Color3.fromRGB(60, 60, 60)
espInd.BackgroundColor3 = _G.ESPEnabled and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(100, 100, 100)
espInd.Position = _G.ESPEnabled and UDim2.new(1, -18, 0, 2) or UDim2.new(0, 2, 0, 2)
toggleESP(_G.ESPEnabled)
end)
boxToggle.MouseButton1Click:Connect(function()
_G.BoxESPEnabled = not _G.BoxESPEnabled
boxToggle.BackgroundColor3 = _G.BoxESPEnabled and Color3.fromRGB(255, 50, 50) or Color3.fromRGB(60, 60, 60)
boxInd.BackgroundColor3 = _G.BoxESPEnabled and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(100, 100, 100)
boxInd.Position = _G.BoxESPEnabled and UDim2.new(1, -18, 0, 2) or UDim2.new(0, 2, 0, 2)
boxESPPreview.Visible = _G.BoxESPEnabled
toggleBoxESP(_G.BoxESPEnabled)
end)
tracerToggle.MouseButton1Click:Connect(function()
_G.TracersEnabled = not _G.TracersEnabled
tracerToggle.BackgroundColor3 = _G.TracersEnabled and Color3.fromRGB(255, 50, 50) or Color3.fromRGB(60, 60, 60)
tracerInd.BackgroundColor3 = _G.TracersEnabled and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(100, 100, 100)
tracerInd.Position = _G.TracersEnabled and UDim2.new(1, -18, 0, 2) or UDim2.new(0, 2, 0, 2)
tracerPreview.Visible = _G.TracersEnabled
toggleTracers(_G.TracersEnabled)
end)
chamToggle.MouseButton1Click:Connect(function()
_G.ChamsEnabled = not _G.ChamsEnabled
chamToggle.BackgroundColor3 = _G.ChamsEnabled and Color3.fromRGB(255, 50, 50) or Color3.fromRGB(60, 60, 60)
chamInd.BackgroundColor3 = _G.ChamsEnabled and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(100, 100, 100)
chamInd.Position = _G.ChamsEnabled and UDim2.new(1, -18, 0, 2) or UDim2.new(0, 2, 0, 2)
chamsPreview.Visible = _G.ChamsEnabled
toggleChams(_G.ChamsEnabled)
end)
-- Input Handling
UserInputService.InputBegan:Connect(function(input)
if input.KeyCode == _G.MenuBindKey then
container.Visible = not container.Visible
end
if _G.AimbotBindEnabled and (input.KeyCode == _G.AimbotBindKey or input.UserInputType == _G.AimbotBindKey) then
    aimbotActive = true
    if not lockedTarget then
        lockedTarget = getClosestTarget()
    end
end
end)
UserInputService.InputEnded:Connect(function(input)
if _G.AimbotBindEnabled and (input.KeyCode == _G.AimbotBindKey or input.UserInputType == _G.AimbotBindKey) then
aimbotActive = false
lockedTarget = nil
end
end)
-- Main Loop
RunService.RenderStepped:Connect(function()
if fovCircle then
local mousePos = UserInputService:GetMouseLocation()
fovCircle.Position = mousePos
end
if _G.AimbotEnabled and (not _G.AimbotBindEnabled or aimbotActive) then
    local target = lockedTarget
    
    if not target or not target.Parent or not target.Parent:FindFirstChild("Humanoid") or target.Parent.Humanoid.Health <= 0 then
        target = getClosestTarget()
        if aimbotActive then
            lockedTarget = target
        end
    end
    
    if target and player.Character then
        local targetPos = target.Position
        local currentCF = Camera.CFrame
        local targetCF = CFrame.new(currentCF.Position, targetPos)
        local smoothness = _G.AimbotSmoothness / 100
        Camera.CFrame = currentCF:Lerp(targetCF, 1 - smoothness)
    end
end

if _G.ESPEnabled then
    for p, d in pairs(espObjects) do
        pcall(function()
            if p.Character and p.Character:FindFirstChild("HumanoidRootPart") and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                local dist = (player.Character.HumanoidRootPart.Position - p.Character.HumanoidRootPart.Position).Magnitude
                
                if dist <= _G.ESPMaxDistance then
                    d.billboard.Enabled = true
                    
                    if _G.ESPShowDistance then
                        d.distanceLabel.Text = math.floor(dist) .. "m"
                    end
                    
                    if _G.ESPShowHealth or _G.ESPHealthBar then
                        local hum = p.Character:FindFirstChild("Humanoid")
                        if hum then
                            local hp = math.floor(hum.Health)
                            local hpPercent = hp / hum.MaxHealth
                            
                            if _G.ESPShowHealth then
                                d.healthLabel.Text = hp .. " HP"
                                d.healthLabel.TextColor3 = Color3.fromRGB(255 * (1 - hpPercent), 255 * hpPercent, 0)
                            end
                            
                            if _G.ESPHealthBar and d.healthBarFill then
                                d.healthBarFill.Size = UDim2.new(hpPercent, 0, 1, 0)
                                d.healthBarFill.BackgroundColor3 = Color3.fromRGB(255 * (1 - hpPercent), 255 * hpPercent, 0)
                            end
                        end
                    end
                else
                    d.billboard.Enabled = false
                end
            end
        end)
    end
end

if _G.TracersEnabled then
    for p, line in pairs(tracerObjects) do
        pcall(function()
            if p.Character and p.Character:FindFirstChild("HumanoidRootPart") and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                local dist = (player.Character.HumanoidRootPart.Position - p.Character.HumanoidRootPart.Position).Magnitude
                
                if dist <= _G.ESPMaxDistance then
                    local pos = p.Character.HumanoidRootPart.Position
                    local screenPos, onScreen = Camera:WorldToScreenPoint(pos)
                    
                    if onScreen then
                        line.Visible = true
                        local startPos = _G.TracerFromBottom and Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y) or Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)
                        line.From = startPos
                        line.To = Vector2.new(screenPos.X, screenPos.Y)
                    else
                        line.Visible = false
                    end
                else
                    line.Visible = false
                end
            end
        end)
    end
end

if _G.ChamsEnabled and _G.ChamsRainbow then
    for p, h in pairs(chamsObjects) do
        pcall(function()
            h.FillColor = Color3.fromHSV(tick() % 5 / 5, 1, 1)
        end)
    end
end
end)
local function setupPlayerESP(p)
if p == player then return end
p.CharacterAdded:Connect(function(char)
    task.wait(0.5)
    
    pcall(function()
        if _G.ESPEnabled then createESP(p) end
        if _G.BoxESPEnabled then createBoxESP(p) end
        if _G.TracersEnabled then createTracerLine(p) end
        if _G.ChamsEnabled then createChams(p) end
    end)
end)

if p.Character then
    task.spawn(function()
        if _G.ESPEnabled then createESP(p) end
        if _G.BoxESPEnabled then createBoxESP(p) end
        if _G.TracersEnabled then createTracerLine(p) end
        if _G.ChamsEnabled then createChams(p) end
    end)
end
end
Players.PlayerAdded:Connect(function(p)
setupPlayerESP(p)
end)
Players.PlayerRemoving:Connect(function(p)
removeESP(p)
removeBoxESP(p)
removeTracer(p)
removeChams(p)
end)
for _, p in pairs(Players:GetPlayers()) do
setupPlayerESP(p)
end
switchTab("Aimbot")
