local Settings = {
  JoinTeam = "Pirates"; -- Pirates/Marines
  Translator = true; -- true/false
}

loadstring(game:HttpGet("https://raw.githubusercontent.com/realredz/BloxFruits/refs/heads/main/Source.lua"))(Settings)

task.spawn(function()
    while task.wait(0.1) do
        pcall(function()
            if not game.Players.LocalPlayer.Character then return end
            if not (game.Players.LocalPlayer.Character:FindFirstChild("EquippedWeapon") and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")) then return end
            local targets = {}
            for _, container in ipairs({workspace.Enemies, workspace.Characters}) do
                for _, v in ipairs(container:GetChildren()) do
                    if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Head") and v:FindFirstChild("Humanoid") and (v:FindFirstChild("HumanoidRootPart").Position - game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart").Position).Magnitude < 50 then
                        targets[#targets+1] = v
                    end
                end
            end
            game:GetService("ReplicatedStorage"):WaitForChild("Modules"):WaitForChild("Net"):WaitForChild("RE/RegisterAttack"):FireServer(-math.huge)
            local args = {targets[1].Head, {}}
            for i, v in ipairs(targets) do
                args[2][i] = {v, v.HumanoidRootPart}
            end
            game:GetService("ReplicatedStorage"):WaitForChild("Modules"):WaitForChild("Net"):WaitForChild("RE/RegisterHit"):FireServer(unpack(args))
        end)
    end
end)
