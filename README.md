# 4º Projeto do Curso de Luau (DIO)

### Module Scripts
##### MathUtils
```Luau
local MathUtils = {}

function MathUtils.Sum(...)
	local numbers = {...}
	local sum = 0
	for i = 1, #numbers do
		sum = sum + numbers[i]
	end
	return sum
end

function MathUtils.Minus(...)
	local numbers = {...}
	local minus = numbers[1]
	for i = 2, #numbers do
		minus = minus - numbers[i]
	end
	return minus
end

function MathUtils.Multiply(...)
	local numbers = {...}
	local product = 1
	for i = 1, #numbers do
		product = product * numbers[i]
	end
	return product
end

function MathUtils.Divide(divident)
	return divident / 2
end

function MathUtils.Square(base)
	return base ^ 2
end

function MathUtils.Mod(number)
	return number % 2
end

return MathUtils
```

##### PlayersUtil

```Luau
local PlayersUtil = {}

function PlayersUtil.GetFriendsInServer()
	local localPlayer = game.Players.LocalPlayer
	local friendsInServer = {}
	for _, player in ipairs(game.Players:GetPlayers()) do
		if player ~= localPlayer then
			local success, isFriends = pcall(function()
				return localPlayer:IsFriendsWith(player.UserId)
			end)
			if success and isFriends then
				table.insert(friendsInServer, player)
			end
		end
	end
	return #friendsInServer
end

function PlayersUtil.GetPlayerQuantity()
	return #game.Players:GetPlayers()
end

return PlayersUtil
```

##### StringUtil
```Luau
local StringUtil = {}

function StringUtil.ToUpperCase(String)
	return string.upper(String)
end

function StringUtil.ToLowerCase(String)
	return string.lower(String)
end

function StringUtil.StringLength(String)
	return string.len(String)
end

function StringUtil.Trim(String)
	return string.gsub(String, "^%s*(.-)%s*$", "%1")
end

return StringUtil
```

### Scripts De Verificação
##### MathUtilsTest
```Luau
local MathUtils = require(script.Parent.MathUtils)

local Number1 = 15
local Number2 = 5
local Number3 = 10

print("====Resultados MathUtils====")
local soma = MathUtils.Sum(Number1, Number2, Number3)
print("Soma: "..soma)

local multiplicacao = MathUtils.Multiply(Number1, Number3)
print("Multiplicação: "..multiplicacao)

local subtracao = MathUtils.Minus(Number1, Number2)
print("Subtração: "..subtracao)

local divisao = MathUtils.Divide(Number1, Number2)
print("Divisão: "..divisao)

local quadrado =  MathUtils.Square(Number3)
print("Quadrado: "..quadrado)

local modulo = MathUtils.Mod(Number1)
print("Mod: "..modulo)
```

##### PlayersUtilTest
```Luau
local PlayersUtil = require(script.Parent.PlayersUtil)

print("====Resultados PlayersUtil====")
local amigos = PlayersUtil.GetFriendsInServer()
print("Existem "..amigos.." players que são seus amigos no server")

local qntPlayers = PlayersUtil.GetPlayerQuantity()
print("Players Online: "..qntPlayers)
```

##### StringUtilTest
```Luau
local StringUtil = require(script.Parent.StringUtil)

print("====Resultados StringUtil====")

print(StringUtil.ToUpperCase("em letra maiuscula"))
local aString = StringUtil.ToLowerCase("EM LETRA MINUSCULA")
print(aString)
print("Tamanho da ultima String: "..StringUtil.StringLength(aString))
print(StringUtil.Trim("         Abóbora        "))
```
