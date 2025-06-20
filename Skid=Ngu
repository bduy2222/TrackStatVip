
-- ✅ Obfuscated version (executor-friendly, webhook+delay config)
local g1 = getgenv
local H = game:GetService("HttpService")
local P = game:GetService("Players").LocalPlayer
local D = P:WaitForChild("Data")

local w = g1().webhook or ""
local t = tonumber(g1().delay) or 60

if w == "" then
    P:Kick("❌ WEBHOOK trống. Gán getgenv().webhook trước.")
    return
end

local function Q(i)
    for _,v in pairs(game.ReplicatedStorage.Remotes.CommF_:InvokeServer("getInventory")) do
        if v.Name == i then return true end
    end
    return false
end

local function M()
    local m = {"Superhuman","DeathStep","SharkmanKarate","ElectricClaw","DragonTalon","GodHuman","SanguineArt"}
    local o = {}
    for _,n in pairs(m) do
        if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("Buy"..n, true) == 1 then
            table.insert(o, n)
        end
    end
    return #o > 0 and table.concat(o,", ") or "Không có"
end

local function R()
    local r = D.Race.Value
    local s = {
        Human="Last Resort", Mink="Agility", Fishman="Water Body",
        Skypiea="Heavenly Blood", Ghoul="Heightened Senses", Cyborg="Energy Core"
    }
    if s[r] and (P.Backpack:FindFirstChild(s[r]) or P.Character:FindFirstChild(s[r])) then
        return r.." V3"
    elseif D.Race:FindFirstChild("Evolved") then
        return r.." V2"
    else
        return r.." V1"
    end
end

local function A()
    local f = D.DevilFruit.Value
    local v = {
        ["Buddha-Buddha"]=true,["Magma-Magma"]=true,["Dark-Dark"]=true,
        ["Dough-Dough"]=true,["Phoenix-Phoenix"]=true,["Flame-Flame"]=true,
        ["Quake-Quake"]=true,["Ice-Ice"]=true,["Rumble-Rumble"]=true,
        ["Light-Light"]=true,["Sand-Sand"]=true,["Spider-Spider"]=true
    }
    if not v[f] then return "Không hỗ trợ" end
    local a = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("getAwakenedAbilities")
    local r = {}
    for _,k in pairs(a) do
        if k.Awakened then table.insert(r, k.Key) end
    end
    return #r > 0 and table.concat(r,", ") or "Chưa awaken"
end

local function F(l)
    local r = {}
    for _,i in ipairs(l) do
        table.insert(r, (Q(i) and "✅" or "❌").." "..i)
    end
    return table.concat(r, "\n")
end

local acc = {"Dark Coat","Ghoul Mask","Swan Glasses","Pale Scarf","Valkyrie Helm"}
local swd = {"Cursed Dual Katana","Tushita","Yama","Shisui","Saber"}
local gun = {"Soul Guitar","Kabucha","Bizarre Rifle"}
local fru = {"Leopard-Leopard","Dough-Dough","Dragon-Dragon","Venom-Venom"}
local mat = {"Mirror Fractal","Dragon Scale","Bones","Dark Fragment"}

while task.wait(t) do
    local d = {
        username = "📊 Blox Fruits Tracker",
        embeds = {{
            title = "Real-Time Info • "..P.Name,
            color = 0x00ccff,
            fields = {
                {name="🏷️ Level",value=D.Level.Value,inline=true},
                {name="💰 Beli",value=D.Beli.Value,inline=true},
                {name="💎 Fragments",value=D.Fragments.Value,inline=true},
                {name="🧬 Race",value=R(),inline=true},
                {name="🥋 Melee",value=M(),inline=false},
                {name="🍎 Fruit",value=D.DevilFruit.Value~="" and D.DevilFruit.Value or "Không có",inline=true},
                {name="⚡ Awaken",value=A(),inline=true},
                {name="🎒 Phụ kiện",value=F(acc),inline=false},
                {name="🗡️ Kiếm",value=F(swd),inline=false},
                {name="🔫 Súng",value=F(gun),inline=false},
                {name="🍏 Trái Mythical",value=F(fru),inline=false},
                {name="🧱 Nguyên liệu",value=F(mat),inline=false}
            },
            footer = { text = "Cập nhật lúc "..os.date("%H:%M:%S %d/%m/%Y") }
        }}
    }

    pcall(function()
        H:PostAsync(w, H:JSONEncode(d), Enum.HttpContentType.ApplicationJson)
    end)
end
