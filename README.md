Configurações locais = {
	['Material'] = Enum.Material.Neon, -- Material
	['Cor'] = Color3.fromRGB(0,255,255), -- Cor
	['Transparência'] = 0,7 -- 0 a 1 Transparência
}

local ScreenGui = Instance.new('ScreenGui', game.CoreGui) -- Cria screengui
ScreenGui.IgnoreGuiInset = verdadeiro

local ViewportFrame = Instance.new('ViewportFrame', ScreenGui) -- Cria viewport e define propriedades
ViewportFrame.CurrentCamera = espaço de trabalho.CurrentCamera
ViewportFrame.Size = UDim2.new(1,0,1,0)
ViewportFrame.BackgroundTransparency = 1
ViewportFrame.ImageTransparency = Configurações.Transparência

Chasms locais = {} -- Matriz para armazenar peças

função generateChasm(player) -- funções que geram abismos para o jogador especificado
	Personagem local = espaço de trabalho:FindFirstChild(jogador.Nome)
	
	se personagem então
		para _,Parte em pares(Character:GetChildren()) faça
			se Part:IsA('Part') ou Part:IsA('MeshPart') então
				Abismo local = Parte:Clone()
				
				para _,Criança em pares(Chasm:GetChildren()) faça
					se Criança:IsA('Decalque') então
						Criança:Destruir()
					fim
				fim
				
				Chasm.Parent = ViewportFrame
				Chasm.Material = Configurações.Material
				Chasm.Color = Configurações.Cor
				Chasm.Anchored = verdadeiro
				
				table.insert(Abismos, Abismo)
			fim
		fim
	fim
fim

função clearChasms() -- remove todos os abismos
	para _,Chasm em pares(Chasms) faça
		Abismo:Destruir()
	fim
	
	Abismos = {}
fim

enquanto jogo:GetService('RunService').RenderStepped:Wait() do -- faz um loop neste processo
	limparChasms()
	
	para _,Jogador em pares(jogo:GetService('Jogadores'):GetPlayers()) faça
		se Jogador ~= jogo:GetService('Jogadores').LocalPlayer então
			gerarChasm(Jogador)
		fim
	fim
fim
