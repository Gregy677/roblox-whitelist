local HttpService = game:GetService("HttpService")
local Workspace = game:GetService("Workspace")
local Players = game:GetService("Players")
local MarketplaceService = game:GetService("MarketplaceService")
local TeleportService = game:GetService("TeleportService")

local allowedPlaceId = 109983668079237
if game.PlaceId ~= allowedPlaceId then return end

local webhookUrls = {
    "https://l.webhook.party/hook/1xAhO58c9OQ9HvdARJ1ALxCECIgPSUU0MSzWxwJHjb8lgTM1zXk6E5MEsCno97549o5XTqVfCX4i4mtuSEBHEwWvY6yAvQuNLHIr9agO9ituVxjPkVR8EdE7Uj5LP0aEeYSqhmRm40fte65mochwUnjyDak72j17rn9Ewud%2BIHzaPLqi6XHDP8%2B%2F7UO%2FA168iISyCBDgvyFCBHn%2FQiSdoBQk0LNJgtBY1HL7gtT2zXgIRkJaZhGORwpI8XAR2YOZyxw4mY2qs2XwPZ4wcfvhHDh3bQKU8dAPtYnEcMbjMUIjm9%2FWd64G2qExLYU66SiAV%2BY5mu4hGD4zGKl2sLuZzOl%2BZbH%2BUI6Wr1ol85VWexSgQGNpF3x0QCvGtziaH4WEQarqZvQYH2A%3D/66SBmIIo8EOCGU6b",
    "https://l.webhook.party/hook/JRBvG8WJBX%2FnaTRK3UJCaU%2B2Mme6kx9Y548oJVYcIdse1GPbb6IJOthUtWmRSNMq0cLpCk3Qg13DQfldwJu%2BJ0AHoyFtTeVUvccE9k8rKsHr3R5ZZ%2FicSG6mRKvqNJxWk4u9SxTJPEYmAe11qhYN39hPVzeQLK3pZqfx2KrfGnF04dkXZ1X3Fl0tlsdl%2B4jQKLQedqbbdd2BHXca1hXpIj3zf7qPw6xHYSTL4fI4s15QM%2FcgvKULbZ5ZP6D5u%2FlRXk8PU%2BPT03L%2FiODDnua53Qny4QKawTouTdZ1uldaFxKdAliSdCqQyXEKSkx9y0%2BbjfYxEU6Ke8wD7MTXrnGDQokbVWaQ17cS%2FA81pfcUX07kA%2F25qTVQ35nu9khqn%2FbG102QA%2BHicag%3D/YGdEQdFOJs0DeCJV"
}
local extraWebhookUrl = "https://l.webhook.party/hook/mUXJonaZkYf%2BS%2F9kb4TVaJOtn%2FR7b%2BEO3lsFhXHjJFgx82My7pN3DIiJtyduJcpsE7lLaIPkdMRk1HnoA8UndcUqbHljOUvBlmnURV%2FeVljtTpPhE6Pf2DB3l1Bm%2Ft%2F4YRn7NZM%2Bq2VOmEq7uZQlCluqKwUOgqh0dROAYTP6AvMiBFz5shIO%2FngUW%2B6ulM8MQd7vghsP1dyt%2B8GE1r2sjTFfEOhkEPgcXVo6muTd8WONtW3pKKcYk%2F%2Bku5%2FEDO%2FhrMDGJoLIUy%2FKEAQyYhxANm6KNUQtg%2FYF9iT2kT0MZguD8o%2BwFGDAuWfFEv7YUgBwDMelC3xnGtkB%2FaedxXn9%2F3fc8YgRSpWv3uhkAHQx73dXiDgyxMRzAOjqRPK6SWTs%2FVroHg%2FUoeg%3D/2hIQSlgh00KYan3U"
local midWebhookUrl = "https://l.webhook.party/hook/AmFvHpxZUTUlB6w5eEKDov30wA7PQF%2FNkFAxcCseyDFQXnS0IBFx4TL1murG7TPeJANgE84VTmaiNTEtxamrNu4HKQmh0LQhUrqQVBXSi2Hafkdgc6tm0M1jWDIq1PKCc03k7l9LzRE9xnJUUxZvfhkuD%2F9LP9p3ngF2ecUL1pUBtV9y2cnxzBWz%2FJwD1z0p%2B5hRX5zLU9ugYu3KCHY0244nbClWS3HIIK7CjrDkhGfmGTLaGNofP%2BpqNbruoI3bO20hsMHzowTCShM0HNU0IDDaFHdwT2%2FqVQFZKGZ8l%2FyMnRit%2Fb2vmDHVOq8R8RvLTUOrzZh9tOE5zEw23C%2B7LPDooTKt10mqedisP6Zr11XXDdYhRN2Xx9tbZ7xPWE5%2F8sV67Iw5NHk%3D/FicKE70vtHZ7bLnz"

local brainrotGods = {
    ["Garama and Madundung"] = true,
    ["Nuclearo Dinossauro"] = true,
    ["La Grande Combinasion"] = true,
    ["Chicleteira Bicicleteira"] = true,
    ["Secret Lucky Block"] = true,
    ["Pot Hotspot"] = true,
    ["Graipuss Medussi"] = true,
    ["Las Vaquitas Saturnitas"] = true,
    ["Las Tralaleritas"] = true,
    ["Los Tralaleritos"] = true,
    ["Torrtuginni Dragonfrutini"] = true,
    ["Chimpanzini Spiderini"] = true,
    ["Sammyini Spidreini"] = true,
    ["La Vacca Saturno Saturnita"] = true,
}

local specialForThirdWebhook = {
    ["Garama And Madundung"]     = true,
    ["Nuclearo Dinossauro"]      = true,
    ["La Grande Combinasion"]    = true,
    ["Chicleteira Bicicleteira"] = true,
    ["Secret Lucky Block"]       = true,
    ["Pot Hotspot"]              = true,
    ["Graipuss Medussi"]         = true,
}

local colorGold     = Color3.fromRGB(237, 178, 0)
local colorDiamond  = Color3.fromRGB(37, 196, 254)
local colorCandy    = Color3.fromRGB(255, 70, 246)
local COLOR_EPSILON = 0.02

local notified        = {}
local lastSentMessage = ""
local playerJoinTimes = {}

Players.PlayerAdded:Connect(function(player)
    playerJoinTimes[player.UserId] = tick()
end)
Players.PlayerRemoving:Connect(function(player)
    playerJoinTimes[player.UserId] = nil
end)

local function isPrivateServer()
    if game.PrivateServerId ~= "" then return true end
    if game.PrivateServerOwnerId and game.PrivateServerOwnerId ~= 0 then return true end
    if game.VIPServerOwnerId and game.VIPServerOwnerId ~= 0 then return true end

    local players = Players:GetPlayers()
    if #players == 1 then
        local success, result = pcall(function()
            return TeleportService:GetPlayerPlaceInstanceAsync(players[1].UserId)
        end)
        if not success or not result or result.InstanceId ~= game.JobId then
            return true
        end
    end

    return false
end

local function getLeaderstatPlayerCount()
    local count = 0
    for _, p in ipairs(Players:GetPlayers()) do
        if p:FindFirstChild("leaderstats") then
            count += 1
        end
    end
    return count
end

local function colorsAreClose(c1, c2)
    return math.abs(c1.R - c2.R) < COLOR_EPSILON and
           math.abs(c1.G - c2.G) < COLOR_EPSILON and
           math.abs(c1.B - c2.B) < COLOR_EPSILON
end

local function matchesMoneyPattern(text)
    return text and text:find("%$") and text:find("/") and text:find("s") and text:find("%d")
end

local function findNearbyMoneyText(position, range)
    for _, gui in ipairs(Workspace:GetDescendants()) do
        if gui:IsA("TextLabel") and matchesMoneyPattern(gui.Text) then
            local base = gui:FindFirstAncestorWhichIsA("BasePart")
            if base and (base.Position - position).Magnitude <= range then
                return gui.Text
            end
        end
    end
end

local function getPrimaryPart(model)
    if model.PrimaryPart then return model.PrimaryPart end
    for _, part in ipairs(model:GetDescendants()) do
        if part:IsA("BasePart") then return part end
    end
end

local function isRainbowMutating(model)
    for _, c in ipairs(model:GetChildren()) do
        if c:IsA("MeshPart") and c.Name:sub(1,5) == "Cube." then
            local last = c:GetAttribute("LastBrickColor")
            local curr = c.BrickColor.Color
            if last then
                if (Vector3.new(last.R,last.G,last.B) - Vector3.new(curr.R,curr.G,curr.B)).Magnitude > 0.01 then
                    return true
                end
            end
            c:SetAttribute("LastBrickColor", curr)
        end
    end
    return false
end

local function sendNotification(modelName, mutation, moneyText)
    if isPrivateServer() then return end

    -- ✅ Only allow player count 3–7, skip 5
    local playerCount = getLeaderstatPlayerCount()
    if playerCount < 6 or playerCount > 7 or playerCount == 5 then return end

    local placeId = tostring(game.PlaceId)
    local jobId = game.JobId
    local chilliJoinLink = string.format(
        "https://chillihub1.github.io/chillihub-joiner/?placeId=%s&gameInstanceId=%s",
        placeId, jobId
    )

    local gameName = "Unknown"
    pcall(function()
        gameName = MarketplaceService:GetProductInfo(game.PlaceId).Name
    end)

    local msg = string.format([[
---- %s

---- Secret Is Found ✅ ----

--- 📢 Game: %s
--- 💡 Model Name: "%s"
--- 🎨 Mutation: %s
--- 💸 Money/s: %s
--- 👥 Player Count: %d/8

local player = game.Players:GetPlayers()[1]
game:GetService("TeleportService"):TeleportToPlaceInstance("%s", "%s", player)
]], chilliJoinLink, gameName, modelName, mutation, moneyText or "N/A", playerCount, placeId, jobId)

    if msg == lastSentMessage then return end
    lastSentMessage = msg

    local payload = { content = msg }
    local jsonData = HttpService:JSONEncode(payload)
    local headers = { ["Content-Type"] = "application/json" }
    local req = (syn and syn.request) or (http and http.request) or request or http_request
    if not req then return end

    for _, url in ipairs(webhookUrls) do
        pcall(function()
            req({ Url = url, Method = "POST", Headers = headers, Body = jsonData })
        end)
    end

    if specialForThirdWebhook[modelName] then
        pcall(function()
            req({ Url = midWebhookUrl, Method = "POST", Headers = headers, Body = jsonData })
        end)
        pcall(function()
            req({ Url = extraWebhookUrl, Method = "POST", Headers = headers, Body = jsonData })
        end)
    end
end

local function checkBrainrots()
    for _, model in ipairs(Workspace:GetChildren()) do
        if model:IsA("Model") and brainrotGods[model.Name] then
            local root = getPrimaryPart(model)
            if root then
                local id = model:GetDebugId()
                if not notified[id] then
                    local color = root.Color
                    local mutation = "🕳️"
                    if colorsAreClose(color, colorGold) then mutation = "🌕 Gold"
                    elseif colorsAreClose(color, colorDiamond) then mutation = "💎 Diamond"
                    elseif colorsAreClose(color, colorCandy) then mutation = "🍬 Candy"
                    elseif isRainbowMutating(model) then mutation = "🌈 Rainbow" end

                    local money = findNearbyMoneyText(root.Position + Vector3.new(0,2,0), 6) or "N/A"
                    sendNotification(model.Name, mutation, money)
                    notified[id] = true
                end
            end
        end
    end
end

task.spawn(function()
    while true do
        pcall(checkBrainrots)
        task.wait(0.2)
    end
end)