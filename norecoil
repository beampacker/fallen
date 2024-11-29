local r = {}
local m = math.random
local w = function()
    while not game.ReplicatedStorage:FindFirstChild("Modules") do wait() end
    while not game.ReplicatedStorage.Modules:FindFirstChild("ToolInfo") do wait() end
    return require(game.ReplicatedStorage.Modules.ToolInfo)
end

local s, u = pcall(w)
if not s then game.Players.LocalPlayer:Kick("Error") return end

local f = function()
    for _, v in pairs(u) do
        if type(v) == "table" and v.Recoil and type(v.Recoil.Camera) == "table" then
            local c = v.Recoil.Camera
            if not r[v] then r[v] = {FinishStart = c.FinishStart} end
            c.FinishStart = m(0, 1) * 0.05
        end
    end
end

setmetatable(u, {
    __index = function(t, k)
        local v = rawget(t, k)
        if type(v) == "table" and v.Recoil and type(v.Recoil.Camera) == "table" then
            local c = v.Recoil.Camera
            return setmetatable(c, {
                __index = function(_, k2)
                    if k2 == "FinishStart" and r[v] then
                        return r[v].FinishStart
                    end
                    return rawget(c, k2)
                end,
                __newindex = function(_, k2, v2)
                    if k2 == "FinishStart" then
                        if r[v] then r[v].FinishStart = v2 end
                    end
                    rawset(c, k2, v2)
                end
            })
        end
        return v
    end
})

f()
