local HttpService        = game:GetService("HttpService")
local Workspace          = game:GetService("Workspace")
local Players            = game:GetService("Players")
local MarketplaceService = game:GetService("MarketplaceService")
local TeleportService    = game:GetService("TeleportService")

local allowedPlaceId = 109983668079237
if game.PlaceId ~= allowedPlaceId then return end

-- Webhook URLs
local webhookUrls = {
    "https://l.webhook.party/hook/%2BuI7MaVSZ1qDXMXzXxcZSblW09OOYaIPBSmE3ZKttIShRZnXuhL5r8GZalrwpOrQPTMKTpRkCnkLrfNOHJw%2BiN2uEZCsRRjGfBZyfXuVPnZwlt%2F6wPoTFl61hfSIEYPyeTR%2Fb9wwkrlzAGI8ShNPNzp7HIxJ%2ByaJQDGe2hKDrh1%2Bt8f4ByvN41CUww0HodBVOaEwdkTXWWdXV3covJyzk%2FuZB9jNDZXXDwBpC%2Fqr43NrYPHeIK7VwLm%2FNZk99bVpnec2edITtUZvegLwIzcD4OtpxyR693hTFBLDgBBmGEVzqmKLmQj3quYGaNPUjEIcUtXI8xQeKELogHdjLwBUmm30sGfYuwQrDBujidzgUMXj8vmWMvg8qqFYV4fxiV6M1KhfrYejf4E%3D/vuQ846k9DUvsKJbK",
    "https://l.webhook.party/hook/wI3nNnRLq3TL%2BzWP4iqeUvWdQbXGCOfSFubKCdEMCeA4%2FpynIcYUt3ddRd8WOKCgcjlWDZlEKkmH8WYU8kddp0QIjBLwxZgrsMP3SQoI0UZ%2FDzqlxlwZeGspJKtucnywiTGWkuGk0Ek6Z4KwGsgT2xXW7p0oDYfB%2FrPnyS3IuA1tgql9hk4%2FMTV%2FI5kycjNSpWkSwagU0Rbn46a3K5AJtEJUgRQxTOcAAp7HDMtrQJmL5MSCW%2FoKRq1y3FIhod%2FQYFYbPuijDOgvRb7yZYGyILd8lB0CghhBsnpwhlkiW3fZGm1SCSrVKGCyQO1DtRi5qTNXNuOgkTWa57mMa5O4tsJkU09fPDP6XlgHfYnjxzL9KiAIYFTSXwbwE%2BjyCUyzpweco31fNP8%3D/CZsJrq8hubij7m0d"
}
local extraWebhookUrl = "https://l.webhook.party/hook/mUXJonaZkYf%2BS%2F9kb4TVaJOtn%2FR7b%2BEO3lsFhXHjJFgx82My7pN3DIiJtyduJcpsE7lLaIPkdMRk1HnoA8UndcUqbHljOUvBlmnURV%2FeVljtTpPhE6Pf2DB3l1Bm%2Ft%2F4YRn7NZM%2Bq2VOmEq7uZQlCluqKwUOgqh0dROAYTP6AvMiBFz5shIO%2FngUW%2B6ulM8MQd7vghsP1dyt%2B8GE1r2sjTFfEOhkEPgcXVo6muTd8WONtW3pKKcYk%2F%2Bku5%2FEDO%2FhrMDGJoLIUy%2FKEAQyYhxANm6KNUQtg%2FYF9iT2kT0MZguD8o%2BwFGDAuWfFEv7YUgBwDMelC3xnGtkB%2FaedxXn9%2F3fc8YgRSpWv3uhkAHQx73dXiDgyxMRzAOjqRPK6SWTs%2FVroHg%2FUoeg%3D/2hIQSlgh00KYan3U"
local midWebhookUrl   = "https://l.webhook.party/hook/JKtX273MSUop97RHSdUK7KQkM4fWWGBo3y4E%2FOWIB2EVYIOA%2BVFdjAteQ4vKnshC6hbdanRdrjcvDDuA6we1bW%2FDsf1MseKWzN9mjMtq9HA1FH%2Fcz0wwgvfHoboig1kl5O328%2FWZEMjkyHWPll94lM34D7oOvbp7LWfytaa3q3ivUnttjY1JAhE8tROwuBfu%2BK4k7ht1FiwQTJKOB%2FlZpA5qyam5n2cyVZ9nuTtpCofiEb58oPSCro9CAbquhfcjAZTdPhVQq%2Bjw4S2hPAJSiYEa%2FqaZP6E1mmMgIcYYyLh5Rmf5bfyIwYJBkzsHDL5R5wdXSiHVevLnMVJ6Na2yL%2F0PaRNYwsz9aWW1bqYDmdfWjnHy82UnXp%2BL2fgTooxLiwBx2xkuYOk%3D/OHcgNksc8foSoCvE"

-- Brainrot models
local brainrotGods = {
    ["dragon cannelloni"] = true,
    ["garama and madundung"] = true,
    ["esok sekolah"] = true,
    ["los hotspotsitos"] = true,
    ["nuclearo dinossauro"] = true,
    ["los combinasionas"] = true,
    ["la grande combinasion"] = true,
    ["chicleteira bicicleteira"] = true,
    ["secret lucky block"] = true,
    ["pot hotspot"] = true,
    ["karkerkar kurkur"] = true,
    ["graipuss medussi"] = true,
    ["las vaquitas saturnitas"] = true,
    ["las tralaleritas"] = true,
    ["los tralaleritos"] = true,
    ["agarrini la palini"] = true,
    ["torrtuginni dragonfrutini"] = true,
    ["chimpanzini spiderini"] = true,
    ["sammyini spidreini"] = true,
    ["la vacca saturno saturnita"] = true,
}

-- Special for mid + extra webhook
local specialForThirdWebhook = {
    ["dragon cannelloni"] = true,
    ["garama and madundung"] = true,
    ["esok sekolah"] = true,
    ["los hotspotsitos"] = true,
    ["nuclearo dinossauro"] = true,
    ["los combinasionas"] = true,
    ["graipuss medussi"] = true,
    ["pot hotspot"] = true,
    ["chicleteira bicicleteira"] = true,
}

-- Colors
local colorGold     = Color3.fromRGB(237, 178, 0)
local colorDiamond  = Color3.fromRGB(37, 196, 254)
local colorCandy    = Color3.fromRGB(255, 70, 246)
local COLOR_EPSILON = 0.02

local notified, moneyLabels = {}

-- Money label detection
local function matchesMoneyPattern(text)
    return text and text:find("%$") and text:find("/") and text:lower():find("s") and text:match("%d")
end

local function registerMoneyLabel(label)
    if label:IsA("TextLabel") and matchesMoneyPattern(label.Text) then
        local base = label:FindFirstAncestorWhichIsA("BasePart")
        if base then moneyLabels[base] = label end
    end
end

Workspace.DescendantAdded:Connect(function(obj)
    if obj:IsA("TextLabel") then registerMoneyLabel(obj) end
end)
for _, obj in ipairs(Workspace:GetDescendants()) do
    if obj:IsA("TextLabel") then registerMoneyLabel(obj) end
end

local function getNearbyMoneyForModel(model)
    local parts = {}
    for _, part in ipairs(model:GetDescendants()) do
        if part:IsA("BasePart") then table.insert(parts, part) end
    end
    local closestDist, closestMoney = 10, nil
    for _, part in ipairs(parts) do
        for base, label in pairs(moneyLabels) do
            if base and base.Parent and label and label.Parent then
                local dist = (base.Position - (part.Position + Vector3.new(0,3,0))).Magnitude
                if dist <= closestDist and matchesMoneyPattern(label.Text) then
                    closestDist = dist
                    closestMoney = label.Text
                end
            end
        end
    end
    return closestMoney and ("💸 " .. closestMoney) or "💸 0/s"
end

local function getPrimaryPart(m)
    if m.PrimaryPart then return m.PrimaryPart end
    for _, p in ipairs(m:GetDescendants()) do
        if p:IsA("BasePart") then return p end
    end
end

local function colorsAreClose(a,b)
    return math.abs(a.R-b.R)<COLOR_EPSILON and math.abs(a.G-b.G)<COLOR_EPSILON and math.abs(a.B-b.B)<COLOR_EPSILON
end

local function isRainbowMutating(m)
    for _, c in ipairs(m:GetChildren()) do
        if c:IsA("MeshPart") and c.Name:sub(1,5)=="Cube." then
            local l = c:GetAttribute("LastBrickColor")
            local cu = c.BrickColor.Color
            if l and (Vector3.new(l.R,l.G,l.B)-Vector3.new(cu.R,cu.G,cu.B)).Magnitude>0.01 then return true end
            c:SetAttribute("LastBrickColor", cu)
        end
    end
end

-- Send webhook function
local function sendWebhookForModel(m)
    local root = getPrimaryPart(m)
    if not root then return end
    local id = m:GetDebugId()
    if notified[id] then return end

    -- Anti-private server + single-player safety
    if game.PrivateServerId or Players.MaxPlayers == 1 then return end

    local col, mut = root.Color, "🕳️"
    if colorsAreClose(col,colorGold) then mut="🌕 Gold"
    elseif colorsAreClose(col,colorDiamond) then mut="💎 Diamond"
    elseif colorsAreClose(col,colorCandy) then mut="🍬 Candy"
    elseif isRainbowMutating(m) then mut="🌈 Rainbow" end

    local money = getNearbyMoneyForModel(m)

    -- Player count from leaderstats
    local playerCount = 0
    for _, p in ipairs(Players:GetPlayers()) do
        if p:FindFirstChild("leaderstats") then playerCount = playerCount+1 end
    end
    if playerCount < 5 or playerCount > 7 then return end

    local placeId, jobId = tostring(game.PlaceId), game.JobId
    local joinLink = string.format(
        "https://chillihub1.github.io/chillihub-joiner/?placeId=%s&gameInstanceId=%s",
        placeId, jobId
    )

    local msg = string.format(
        "---- %s\n---- Secret Is Bot Found ✅ ----\n--- 💡 Model Name: \"%s\"\n--- 🎨 Mutation: %s\n--- %s\n--- 👥 Player Count: 8/%d",
        joinLink, m.Name, mut, money, playerCount
    )

    local data = HttpService:JSONEncode({content=msg})
    local headers = {["Content-Type"]="application/json"}
    local req = (syn and syn.request) or (http and http.request) or request or http_request
    if not req then return end

    local nameLower = m.Name:lower()
    if nameLower=="la grande combinasion" then
        for _, url in ipairs(webhookUrls) do pcall(function() req({Url=url,Method="POST",Headers=headers,Body=data}) end) end
        pcall(function() req({Url=midWebhookUrl,Method="POST",Headers=headers,Body=data}) end)
        pcall(function() req({Url=extraWebhookUrl,Method="POST",Headers=headers,Body=data}) end)
    elseif specialForThirdWebhook[nameLower] then
        pcall(function() req({Url=midWebhookUrl,Method="POST",Headers=headers,Body=data}) end)
        pcall(function() req({Url=extraWebhookUrl,Method="POST",Headers=headers,Body=data}) end)
    elseif brainrotGods[nameLower] then
        for _, url in ipairs(webhookUrls) do pcall(function() req({Url=url,Method="POST",Headers=headers,Body=data}) end) end
    end

    notified[id]=true
end

-- Scanners
task.spawn(function()
    while true do
        for _, m in ipairs(Workspace:GetChildren()) do
            if m:IsA("Model") and brainrotGods[m.Name:lower()] then
                pcall(sendWebhookForModel, m)
            end
        end
        task.wait(0.6)
    end
end)

task.spawn(function()
    while true do
        for _, m in ipairs(Workspace:GetChildren()) do
            if m:IsA("Model") and specialForThirdWebhook[m.Name:lower()] then
                pcall(sendWebhookForModel, m)
            end
        end
        task.wait(0.05)
    end
end)