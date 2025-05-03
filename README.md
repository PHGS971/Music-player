# Music Player Script para Roblox

## Descrição

Este script cria uma **GUI de Music Player** no Roblox, permitindo que os jogadores toquem músicas personalizadas a partir de IDs de áudio do Roblox. O usuário pode inserir um ID de música e pressionar o botão "Tocar" para começar a reprodução. Este script é ideal para jogos em que você deseja adicionar uma funcionalidade de música personalizada de forma simples e eficiente.

## Funcionalidades

- **Interface gráfica** simples e intuitiva.
- **Campo de texto** para inserir o ID do áudio da música.
- **Botão de "Tocar"** para iniciar a música a partir do ID fornecido.
- **Notificações** para confirmar a execução ou alertar sobre erros com IDs inválidos.

## Como Usar

1. **Carregue o script** no seu jogo Roblox.
2. **Execute o script** para criar a interface do Music Player.
3. **Insira o ID de uma música** do Roblox no campo de texto.
4. **Pressione o botão "Tocar"** para ouvir a música.
5. Caso o ID seja inválido, uma notificação de erro será exibida.

## Exemplo de Código

```lua
-- Music Player Script

-- Criar a GUI do Music Player
local ScreenGui = Instance.new("ScreenGui", game.Players.LocalPlayer:WaitForChild("PlayerGui"))
local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 200, 0, 120)
Frame.Position = UDim2.new(0.5, -100, 0.5, -60)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)

local TextBox = Instance.new("TextBox", Frame)
TextBox.PlaceholderText = "Digite o ID da música"
TextBox.Size = UDim2.new(1, -20, 0, 30)
TextBox.Position = UDim2.new(0, 10, 0, 10)

local PlayButton = Instance.new("TextButton", Frame)
PlayButton.Text = "Tocar"
PlayButton.Size = UDim2.new(1, -20, 0, 30)
PlayButton.Position = UDim2.new(0, 10, 0, 50)

local Sound = Instance.new("Sound", game.SoundService)
Sound.Volume = 1

PlayButton.MouseButton1Click:Connect(function()
    local id = TextBox.Text
    if tonumber(id) then
        Sound.SoundId = "rbxassetid://" .. id
        Sound:Play()
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "Tocando Música",
            Text = "Música iniciada com sucesso!",
            Duration = 3
        })
    else
        warn("ID inválido")
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "Erro",
            Text = "Por favor, insira um ID de música válido.",
            Duration = 3
        })
    end
end)
